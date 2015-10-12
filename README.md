NUDGE
=====

A simple tool for telling an idle service to wake up and "do it's thing"

For example, you have a terminal window open on `computer1` where you want to
monitor disk space free in `/tmp`. You could use a `while sleep 1` loop, or you
could use *nudge* to redraw the screen only when necessary:

    # computer 1 (192.168.1.1)
    $ while nudge --listen 11111; do clear; df -h /tmp; done

    # computer 2
    $ for f in *.tar.gz; do scp $f computer1:/tmp/; nudge 192.168.1.1 11111; done


Example 2: You want to rerun your unit tests in a separate terminal window each
time you press `F5` in vim:

    # terminal 1 (unit tests)
    $ while nudge --listen /tmp/my_unit_tests.sock; do clear; py.test *; done

    # terminal 2 (vim)
    :nnoremap <F5> :silent !nudge - /tmp/my_unit_tests.sock<CR>
