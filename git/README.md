# git

Version control.

## GitHub Email Address (noreply)

As Git requires an email to be attached to commits, it is recommended to use the one provided by GitHub.

Generally speaking, accounts with `Keep my email address private` enabled since before July 18, 2017 have a noreply email address of the form `USERNAME@users.noreply.github.com`. If that setting was enabled or toggled from July 18, 2017 onwards, the form is `ID+USERNAME@users.noreply.github.com`, visible in the GitHub settings under `Emails`.

See [the documentation](https://docs.github.com/en/account-and-profile/reference/email-addresses-reference#your-noreply-email-address) for details.

## Name and Email Variables

In order to do almost anything with Git, a username and email must be configured manually.

Set in the environment, for example those for my account `xenago` would be:

    GIT_AUTHOR_EMAIL=xenago@users.noreply.github.com
    GIT_COMMITTER_EMAIL=xenago@users.noreply.github.com
    GIT_AUTHOR_NAME="xenago"
    GIT_COMMITTER_NAME="xenago"

Set for a single command:

    git -c user.name="xenago" -c user.email="xenago@users.noreply.github.com" commit -m "message"

Set for a repo:

    git config user.email "xenago@users.noreply.github.com"

Set globally:

    git config --global user.name "xenago"  
    git config --global user.email "xenago@users.noreply.github.com" 

Check the configuration values:

    git config user.email
    git config --get user.email 
