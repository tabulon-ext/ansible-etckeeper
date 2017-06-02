# sourcejedi.etckeeper #

Install etckeeper.  Track the contents of /etc using a version control system.

The current contents of `/etc` is recorded in a Git repository.  Etckeeper creates new commits to the repository at daily intervals, and also when files are created or altered by the package manager.

## Status

This particular role was written to work on an existing system.  It has been tested to work regardless of whether

* etckeeper has already been installed
* the etckeeper repository exists or not
* the etckeeper repository happens to exist but without any commits

Ansible `--check` mode is supported.

If you run check mode when etckeeper is not fully installed, the play will fail.  This behaviour is expected, as a complex role where some tasks depend on earlier ones.  We take care to produce this behaviour, making sure that check mode doesn't skip certain types of task and then give a [misleading report of "changed=0"](https://stackoverflow.com/questions/42602154/idioms-for-using-the-command-module).

## Requirements

Used sucessfully on Fedora, Debian, and Ubuntu 16.04+.  I imagine most Linux distributions will provide an etckeeper package that works fine with this role.

Some older version of Ubuntu won't work, because their packaging changed the default backend to `bzr`, instead of `git`.  Etckeeper recommends against this - the backend should be `git`, unless the user has a strong preference for something else.  This role is implemented for `git` specifically (see below).  I might accept minimal pull requests for alternatives.

## Dependencies

`user.email` is set automatically for the git repository.  I didn't include a role variable for it.  However if `user.email` is already set (e.g. in `/root/.gitconfig`), this step is skipped.  So if you care about this, make sure your `/root/.gitconfig` is set up in advance.  (Or send me an issue / pull request, to explain why you want a role variable).


## License

This role is licensed GPLv3, please open an issue if this creates any problem.