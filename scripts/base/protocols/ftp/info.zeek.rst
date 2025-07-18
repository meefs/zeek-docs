:tocdepth: 3

base/protocols/ftp/info.zeek
============================
.. zeek:namespace:: FTP

Defines data structures for tracking and logging FTP sessions.

:Namespace: FTP
:Imports: :doc:`base/protocols/ftp/utils-commands.zeek </scripts/base/protocols/ftp/utils-commands.zeek>`

Summary
~~~~~~~
Runtime Options
###############
=============================================================================== ==========================================================
:zeek:id:`FTP::default_capture_password`: :zeek:type:`bool` :zeek:attr:`&redef` This setting changes if passwords used in FTP sessions are
                                                                                captured or not.
=============================================================================== ==========================================================

Types
#####
========================================================== ==============================================
:zeek:type:`FTP::ExpectedDataChannel`: :zeek:type:`record` The expected endpoints of an FTP data channel.
:zeek:type:`FTP::Info`: :zeek:type:`record`                
========================================================== ==============================================


Detailed Interface
~~~~~~~~~~~~~~~~~~
Runtime Options
###############
.. zeek:id:: FTP::default_capture_password
   :source-code: base/protocols/ftp/info.zeek 11 11

   :Type: :zeek:type:`bool`
   :Attributes: :zeek:attr:`&redef`
   :Default: ``F``

   This setting changes if passwords used in FTP sessions are
   captured or not.

Types
#####
.. zeek:type:: FTP::ExpectedDataChannel
   :source-code: base/protocols/ftp/info.zeek 14 24

   :Type: :zeek:type:`record`


   .. zeek:field:: passive :zeek:type:`bool` :zeek:attr:`&log`

      Whether PASV mode is toggled for control channel.


   .. zeek:field:: orig_h :zeek:type:`addr` :zeek:attr:`&log`

      The host that will be initiating the data connection.


   .. zeek:field:: resp_h :zeek:type:`addr` :zeek:attr:`&log`

      The host that will be accepting the data connection.


   .. zeek:field:: resp_p :zeek:type:`port` :zeek:attr:`&log`

      The port at which the acceptor is listening for the data
      connection.


   The expected endpoints of an FTP data channel.

.. zeek:type:: FTP::Info
   :source-code: base/protocols/ftp/info.zeek 26 78

   :Type: :zeek:type:`record`


   .. zeek:field:: ts :zeek:type:`time` :zeek:attr:`&log`

      Time when the command was sent.


   .. zeek:field:: uid :zeek:type:`string` :zeek:attr:`&log`

      Unique ID for the connection.


   .. zeek:field:: id :zeek:type:`conn_id` :zeek:attr:`&log`

      The connection's 4-tuple of endpoint addresses/ports.


   .. zeek:field:: user :zeek:type:`string` :zeek:attr:`&log` :zeek:attr:`&default` = ``"<unknown>"`` :zeek:attr:`&optional`

      User name for the current FTP session.


   .. zeek:field:: password :zeek:type:`string` :zeek:attr:`&log` :zeek:attr:`&optional`

      Password for the current FTP session if captured.


   .. zeek:field:: command :zeek:type:`string` :zeek:attr:`&log` :zeek:attr:`&optional`

      Command given by the client.


   .. zeek:field:: arg :zeek:type:`string` :zeek:attr:`&log` :zeek:attr:`&optional`

      Argument for the command if one is given.


   .. zeek:field:: mime_type :zeek:type:`string` :zeek:attr:`&log` :zeek:attr:`&optional`

      Sniffed mime type of file.


   .. zeek:field:: file_size :zeek:type:`count` :zeek:attr:`&log` :zeek:attr:`&optional`

      Size of the file if the command indicates a file transfer.


   .. zeek:field:: reply_code :zeek:type:`count` :zeek:attr:`&log` :zeek:attr:`&optional`

      Reply code from the server in response to the command.


   .. zeek:field:: reply_msg :zeek:type:`string` :zeek:attr:`&log` :zeek:attr:`&optional`

      Reply message from the server in response to the command.


   .. zeek:field:: data_channel :zeek:type:`FTP::ExpectedDataChannel` :zeek:attr:`&log` :zeek:attr:`&optional`

      Expected FTP data channel.


   .. zeek:field:: cwd :zeek:type:`string` :zeek:attr:`&default` = ``"."`` :zeek:attr:`&optional`

      Current working directory that this session is in.  By making
      the default value '.', we can indicate that unless something
      more concrete is discovered that the existing but unknown
      directory is ok to use.


   .. zeek:field:: cmdarg :zeek:type:`FTP::CmdArg` :zeek:attr:`&optional`

      Command that is currently waiting for a response.


   .. zeek:field:: pending_commands :zeek:type:`FTP::PendingCmds`

      Queue for commands that have been sent but not yet responded
      to are tracked here.


   .. zeek:field:: command_seq :zeek:type:`count` :zeek:attr:`&default` = ``0`` :zeek:attr:`&optional`

      Sequence number of previous command.


   .. zeek:field:: passive :zeek:type:`bool` :zeek:attr:`&default` = ``F`` :zeek:attr:`&optional`

      Indicates if the session is in active or passive mode.


   .. zeek:field:: capture_password :zeek:type:`bool` :zeek:attr:`&default` = :zeek:see:`FTP::default_capture_password` :zeek:attr:`&optional`

      Determines if the password will be captured for this request.


   .. zeek:field:: fuid :zeek:type:`string` :zeek:attr:`&optional` :zeek:attr:`&log`

      File unique ID.


   .. zeek:field:: last_auth_requested :zeek:type:`string` :zeek:attr:`&optional`

      (present if :doc:`/scripts/base/protocols/ftp/gridftp.zeek` is loaded)




