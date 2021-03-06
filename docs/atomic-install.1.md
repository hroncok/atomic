% ATOMIC(1) Atomic Man Pages
% Dan Walsh
% January 2015
# NAME
atomic-install - Execute Image Install Method

# SYNOPSIS
**atomic install**
[**-h**]
[**--name**[=*NAME*]]
IMAGE [ARG...]

# DESCRIPTION
**atomic install** attempts to read the `LABEL INSTALL` field in the container
IMAGE, if this field does not exist, `atomic install` will install the IMAGE

If the container image has a LABEL INSTALL instruction like the following:

```LABEL INSTALL /usr/bin/docker run -t -i --rm \${OPT1} --privileged -v /:/host --net=host --ipc=host --pid=host -e HOST=/host -e NAME=${NAME} -e IMAGE=${IMAGE} -e CONFDIR=${CONFDIR} -e LOGDIR=${LOGDIR} -e DATADIR=${DATADIR} --name ${NAME} ${IMAGE} \${OPT2} /bin/install.sh \${OPT3}```

`atomic install` will set the following environment variables for use in the command:

**NAME**
  The name specified via the command.  NAME will be replaced with IMAGE if it is not specified.

**IMAGE**
  The name and image specified via the command.

**OPT1, OPT2, OPT3**
  Additional options which can be specified via the command.

**SUDO_UID**
  The `SUDO_UID` environment variable.  This is useful with the docker `-u` option for user space tools.  If the environment variable is not available, the value of `/proc/self/loginuid` is used.

**SUDO_GID**
  The `SUDO_GID` environment variable.  This is useful with the docker `-u` option for user space tools.  If the environment variable is not available, the default GID of the value for `SUDO_UID` is used.  If this value is not available, the value of `/proc/self/loginuid` is used.

`atomic install` will also pass in the CONFDIR, LOGDIR and DATADIR environment variables to the container.  Any additional arguments will be appended to the command.

# OPTIONS:
**--help**
  Print usage statement

**--name**=""
   Use this name for creating installed content for the container.
NAME will default to the IMAGENAME if it is not specified.

# HISTORY
January 2015, Originally compiled by Daniel Walsh (dwalsh at redhat dot com)
