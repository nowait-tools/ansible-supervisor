Supervisor
=========

Supervisor role that installs and configures supervisor.

Requirements
------------

Role Variables
--------------
For more information, see defaults/main.yml

        supervisor_owner: root
        supervisor_group: root

        supervisor_unix_http_server:
          ## (the path to the socket file)
          file: /tmp/supervisor.sock
          ## socket file mode (default 0700)
          chmod: 0700
          ## socket file uid:gid owner
          chown: nobody:nogroup
          ## (default is no username (open server))
          username: user
          ## (default is no password (open server))
          password: 123

        # inet (TCP) server disabled by default
        supervisor_inet_http_server:
          ## (ip_address:port specifier, *:port for all iface)
          port: 127.0.0.1:9001
          ## (default is no username (open server))
          username: user
          ## (default is no password (open server))
          password: 123

        supervisor_supervisord:
          ## (main log file;default $CWD/supervisord.log)
          logfile: /var/log/supervisor/supervisord.log
          ## (supervisord pidfile;default supervisord.pid)
          pidfile: /var/run/supervisord.pid
          ## ('AUTO' child log dir, default $TEMP)
          childlogdir: /var/log/supervisor
          ## (max main logfile bytes b4 rotation;default 50MB)
          logfile_maxbytes: 50mb
          ## (num of main logfile rotation backups;default 10)
          logfile_backups: 10
          ## (log level;default info; others: debug,warn,trace)
          loglevel: info
          ## (start in foreground if true;default false)
          nodaemon: false
          ## (min. avail startup file descriptors;default 1024)
          minfds: 1024
          ## (min. avail process descriptors;default 200)
          minprocs: 200
          ## (process file creation umask;default 022)
          umask: 022
          ## (default is current user, required if root)
          user: user
          ## (supervisord identifier, default is 'supervisor')
          identifier: supervisor
          ## (default is not to cd during start)
          directory: /tmp
          ## (don't clean up tempfiles at start;default false)
          nocleanup: true
          ## (key value pairs to add to environment)
          environment: KEY="value"
          ## (strip ansi escape codes in logs; def. false)
          strip_ansi: false

        supervisor_supervisorctl:
          ## use a unix:// URL  for a unix socket
          serverurl: unix:///tmp/supervisor.sock
          ## use an http:// url to specify an inet socket
          serverurl: http://127.0.0.1:9001
          ## should be same as http_username if set
          username: user
          ## should be same as http_password if set
          password: 123
          ## cmd line prompt (default "supervisor")
          prompt: mysupervisor
          ##  use readline history if available
          history_file: ~/.sc_history

        supervisor_programs:
          - theprogramname:
              ## the program (relative uses PATH, can take args)
              command: /bin/cat
              ## process_name expr (default %(program_name)s)
              process_name: %(program_name)s
              ## number of processes copies to start (def 1)
              numprocs: 1
              ## directory to cwd to before exec (def no cwd)
              directory: /tmp
              ## umask for process (default None)
              umask: None
              ## the relative start priority (default 999)
              priority: 999
              ## start at supervisord start (default: true)
              autostart: true
              ## whether/when to restart (default: unexpected)
              autorestart: unexpected
              ## number of secs prog must stay running (def. 1)
              startsecs: 1
              ## max # of serial start failures (default 3)
              startretries: 3
              ## 'expected' exit codes for process (default 0,2)
              exitcodes: 0,2
              ## signal used to kill process (default TERM)
              stopsignal: TERM
              ## max num secs to wait b4 SIGKILL (default 10)
              stopwaitsecs: 10
              ## send stop signal to the UNIX process group (default false)
              stopasgroup: false
              ## SIGKILL the UNIX process group (def false)
              killasgroup: false
              ## setuid to this UNIX account to run the program
              user: user
              ## redirect proc stderr to stdout (default false)
              redirect_stderr: false
              ## stdout log path, NONE for none; default AUTO
              stdout_logfile: AUTO
              ## max # logfile bytes b4 rotation (default 50MB)
              stdout_logfile_maxbytes: 50MB
              ## # of stdout logfile backups (default 10)
              stdout_logfile_backups: 10
              ## number of bytes in 'capturemode' (default 0)
              stdout_capture_maxbytes: 0MB
              ## emit events on stdout writes (default false)
              stdout_events_enabled: false
              ## stderr log path, NONE for none; default AUTO
              stderr_logfile: AUTO
              ## max # logfile bytes b4 rotation (default 50MB)
              stderr_logfile_maxbytes: 50MB
              ## # of stderr logfile backups (default 10)
              stderr_logfile_backsup: 10
              # ## number of bytes in 'capturemode' (default 0)
              stderr_capture_maxbytes: 0MB
              ## emit events on stderr writes (default false)
              stderr_events_enabled: false
              ## process environment additions (def no adds)
              environment: A=1,B=2
              ## override serverurl computation (childutils)
              serverurl: AUTO

          supervisor_eventlisteners:
            - theeventlistenername:
              ## the program (relative uses PATH, can take args)
              command: /bin/eventlistener
              ## process_name expr (default %(program_name)s)
              process_name: %(program_name)s
              ## number of processes copies to start (def 1)
              numprocs: 1
              ## event notif. types to subscribe to (req'd)
              events: EVENT
              ## event buffer queue size (default 10)
              buffer_size: 10
              ## directory to cwd to before exec (def no cwd)
              directory: /tmp
              ## umask for process (default None)
              umask: None
              ## the relative start priority (default -1)
              priority: -1
              ## start at supervisord start (default: true)
              autostart: true
              ## whether/when to restart (default: unexpected)
              autorestart: unexpected
              ## number of secs prog must stay running (def. 1)
              startsecs: 1
              ## max # of serial start failures (default 3)
              startretries: 3
              ## 'expected' exit codes for process (default 0,2)
              exitcodes: 0,2
              ## signal used to kill process (default TERM)
              stopsignal:QUIT
              ## max num secs to wait b4 SIGKILL (default 10)
              stopwaitsecs: 10
              ## send stop signal to the UNIX process group (default false)
              stopasgroup: false
              ## SIGKILL the UNIX process group (def false)
              killasgroup: false
              ## setuid to this UNIX account to run the program
              user: user
              ## redirect proc stderr to stdout (default false)
              redirect_stderr: true
              ## stdout log path, NONE for none; default AUTO
              stdout_logfile: /a/path
              ## max # logfile bytes b4 rotation (default 50MB)
              stdout_logfile_maxbytes: 50MB
              ## # of stdout logfile backups (default 10)
              stdout_logfile_backups: 10
              ## emit events on stdout writes (default false)
              stdout_events_enabled: false
              ## stderr log path, NONE for none; default AUTO
              stderr_logfile: AUTO
              ## max # logfile bytes b4 rotation (default 50MB)
              stderr_logfile_maxbytes: 50MB
              ## # of stderr logfile backups (default 10)
              stderr_logfile_backups: 10
              ## emit events on stderr writes (default false)
              stderr_events_enabled: false
              ## process environment additions
              environment: A=1,B=2
              ## override serverurl computation (childutils)
              serverurl: AUTO

          supervisor_groups:
            - thegroupname:
            ## each refers to 'x' in [program:x] definitions
            programs: progname1,progname2
            ## the relative start priority (default 999)
            priority: 999

          supervisor_include:
            files: relative/directory/*.init



Example Playbook
----------------

        ---
        - hosts: all
          sudo: yes
          vars:
            supervisor_programs:
              - sample-program-1:
                  command: /bin/cat
                  directory: /tmp
                  environment: A=1,B=2
              - sample-program-2
                  command: /bin/ls
                  directory: /tmp
                  user: root
          roles:
            - nowait-tools.supervisor-ansible


License
-------

MIT

Author Information
------------------

Produced by NoWait
