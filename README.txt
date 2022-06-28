NAME
        watchrun - A wrapper around "watchman-make ... --run ..."
SYNOPSIS
        watchrun PATTERN [PATTERN ...] [--[no-]initial-run] -- COMMAND [ARGS]
DESCRIPTION
        Wraps "watchman-make ... --run ..." so that the arguments to the
        flag "--run" do not need to be quoted or escaped.
        The call from the SYNOPSIS above, exluding the --initial-run flag, is
            mostly equivalent to the following:
        watchman-make -p PATTERN [PATTERN ...] --run "COMMAND_and_ARGS"
        Differences include:
          * by default, an initial run of COMMAND_and_ARGS is performed
            before invoking watchman-make. This can be disabled with the
            --no-initial-run flag.
OPTIONS
        --initial-run
        --no-initial-run
            This option, enabled by default, triggers an initial run of
            "COMMAND [ ARGS ]" before watchman-make is invoked. A failure of
            the initial run does not prevent subsequent runs.
        --redexit
        --no-redexit
            This option, enabled by default, appends message in red text
            if the command failed.
        --greenexit
        --no-greenexit
            This option, enabled by default, appends message in green text
            if the command succeeded.
EXAMPLES
        watchrun 'scripts/*' '*.yaml' --no-initial-run -- pytest -k 'pytest pattern'
            This should be precisely equivalent to the following:
        watchman-make -p 'scripts/*' '*.yaml' --run "pytest -k 'pytest pattern'"
