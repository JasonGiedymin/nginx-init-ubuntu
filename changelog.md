# nginx-init-ubuntu

* v3.7.0
  - Missing reload action from service (@violuke), Fixes #15
  - Add NGINXPATH var (@mattbearman), Fixes #14
  - Version bump

* v3.6.0 - Testing framework, simple deployment script, Fix #8
  - Add Vagrantfile
  - Add `deploy-nginx.yml` which is a simple ansible deployment script
  - Add `integration-tests.yml` which check for service and response
  - Add `.gitignore` entry for `.vagrant`
  - Fix #8 - Error return code now correctly returns when nginx fails to start

* v3.5.1 - Fix #2, part 2
  - Add `log_end_msg` repr (back) for friendly display but make exit codes proper
  - Add exit codes at eos
  - Modify `reload` to properly do send `kill -HUP` like in `quietupgrade`

* v3.5.0 - Fix #2
  - Fix sample install instructions
  - Fix var for quiet upgrade
  - Update documentation with 1.4.3 compatibility
  - Add additional lsb logging
  - Add error codes for `status`, `terminate`, `start`, `stop`, `reload`, `quietupgrade`, `destroy`

* v?.?.?
  - check git commit history :-)
