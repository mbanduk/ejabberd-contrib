

	mod_muc_admin - Administrative features for MUC

	Homepage: http://www.ejabberd.im/mod_muc_admin
	Author: Badlop
	Requirements: ejabberd trunk SVN 1699 or newer


This module implements several ejabberd commands that can be
executed using ejabberdctl.

It also implements Web Admin pages to view the list of existing
rooms.


	CONFIGURATION
	=============

Add the module to your ejabberd.cfg, on the modules section:
modules:
  ...
  mod_muc_admin: {}
  ...



	EJABBERD COMMANDS
	=================

  Command Name: muc_online_rooms
  Arguments: host::binary
  Returns: rooms::[ room::string ]
  Description:  List existing rooms ('global' to get all vhosts)


  Command Name: muc_unregister_nick
  Arguments: nick::binary
  Returns: res::rescode
  Description:  Unregister the nick in the MUC service


  Command Name: does_room_exist
  Arguments: name::binary
             service::binary
  Returns: res::rescode
  Description:  Check if a room name@service exists


  Command Name: create_room
  Arguments: name::binary
             service::binary
             host::binary
  Returns: res::rescode
  Description:  Create a MUC room name@service in host


  Command Name: destroy_room
  Arguments: name::binary
             service::binary
             host::binary
  Returns: res::rescode
  Description:  Destroy a MUC room


  Command Name: create_rooms_file
  Arguments: file::string
  Returns: res::rescode
  Description:  Create the rooms indicated in file


  Command Name: destroy_rooms_file
  Arguments: file::string         
  Returns: res::rescode
  Description:  Destroy the rooms indicated in file


  Command Name: rooms_unused_list
  Arguments: host::binary
             days::integer
  Returns: rooms::[ room::string ]
  Description:  List the rooms that are unused for many days in host

  Command Name: rooms_unused_destroy
  Arguments: host::binary
             days::integer
  Returns: rooms::[ room::string ]
  Description:  Destroy the rooms that are unused for many days in host


  Command Name: get_room_occupants
  Arguments: name::binary
             service::binary
  Returns: occupants::[ occupant::{ jid::string,
                                    nick::string,
                                    role::string } ]
  Description:  Get the list of occupants of a MUC room


  Command Name: get_room_occupants_number
  Arguments: name::binary
             service::binary
  Returns: occupants::integer
  Description:  Get the number of occupants of a MUC room


  Command Name: send_direct_invitation
  Arguments: room::binary
             password::binary
             reason::binary
             users::string
             
  Returns: res::rescode
  Description:  Send a direct invitation to several destinations. Password and Message can also be: none. Users JIDs are separated with :


  Command Name: change_room_option
  Arguments: name::binary
             service::binary
             option::string
             value::string
  Returns: res::rescode
  Description:  Change an option in a MUC room


  Command Name: set_room_affiliation
  Arguments: name::binary
             service::binary
             jid::binary
             affiliation::string             
  Returns: res::rescode
  Description:  Change an affiliation in a MUC room


  Command Name: get_room_affiliations
  Arguments: name::binary
             service::binary
  Returns: affiliations::[ affiliation::{ username::string,
                                          domain::string,
                                          affiliation::string,
                                          reason::string } ]
  Description:  Get the list of affiliations of a MUC room



  Command Name: send_system_message
  Arguments: name::binary
             service::binary
             message::binary
             
  Returns: res::rescode
  Description:  Send a system message to a room

Notes:

 For all muc-unusued-* commands related to MUC require an ejabberd version newer than 1.1.x.
   The room characteristics used to decide if a room is unusued:
    - Days since the last message or subject change:
        greater or equal to the command argument
    - Number of participants: 0
    - Persistent: not important
    - Has history: not important
    - Days since last join, leave, room config or affiliation edit:
        not important
    - Just created: no
   Note that ejabberd does not keep room history after a module restart, so
   the history of all rooms is emtpy after a module or server start.

