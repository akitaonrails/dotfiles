## Dotfiles for WebDevBox

This dotfiles repo was made to be used in my Distrobox image ["WebDevBox"](https://github.com/akitaonrails/webdevbox).

You should fork this to make your own changes. Once you do, install [Chezmoi](https://www.chezmoi.io/) is you're not using my WebDevBox and initialize it like this:

    $ chezmoi init <git@your dotfiles fork url>

It will prompt you for information that will be saved in this local file:

    $ cat ~/.config/chezmoi/chezmoi.toml

All the pulled templates will be here:

    $ ls ~/.local/share/chezmoi

The idea is that it will use the template `dot_zshrc.tmpl`, for example, merge with the data in `chezmoi.toml` and generate your `~/.zshrc`.

Now, just remember to always edit your dotfiles templates. Chezmoi give you some helpers:

    $ chezmoi cd # will cd you to the dotfiles repo directory
    $ chezmoi edit ~/.zshrc # will open the template in your editor

If you create new dotfiles, let's say you started to use Fish, then don't forget to add it to Chezmoi like this:

    $ chezmoi add --autotemplate ~/.fishrc

If you have confidential information that would be bad to show up in your GitHub repository, make sure you first added it to the data file, something like this:

    [data.user.google]
    password = something-something

Then, when you add the file with `autotemplate`, the template will do its magic and this is what will end up in the repo:

    export GOOGLE_PASSWORD={{ .user.google.password }}

You can check your data with:

    $ chezmoi data

Whenever you change the template or the data file, just update everything:

    $ chezmoi update

And then push the changes to your repo:

    $ chezmoi cd
    $ git add .
    $ git commit -m "Update dotfiles"
    $ git push

This should make for a much sane way to manage your dotfiles.
