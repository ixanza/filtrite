## filtrite
filtrite is a project for generating filter lists for [Bromite](https://www.bromite.org/).
See the page about [Custom Ad Block Filters](https://www.bromite.org/custom-filters) for more info.

# Lists
You can choose any list from the table, then hold the name to copy its link. Add it to Bromite by going to settings > AdBlock settings, then setting "Filters URL" to the link you just copied.

| Link | Description  |
| ------ | ------|
| [Bromite Default](https://github.com/ixanza/filtrite/releases/latest/download/bromite-default.dat) | Bromite [default filter list](https://github.com/bromite/filters), but generated by this tool |
| [Bromite Custom](https://github.com/ixanza/filtrite/releases/latest/download/bromite-custom.dat) | The default list with additional annoyance blockers I use with [uBlock Origin](https://github.com/gorhill/uBlock) on Desktop |

These lists are regularly updated automatically using GitHub Actions.

**Note**: I'm not 100% sure if all list formats that are used are actually supported by [the ruleset generation tool](https://github.com/xarantolus/subresource_filter_tools) (as the output indicates some failures). If you have a comment on that, please open an issue :)

### Advanced blocking
The normal Bromite ad blocking engine does not support all blocking formats. However, since the introduction of user scripts, it has become possible to block even more annoying elements. If you want more blockers (e.g. for cookie prompts), see my [custom Bromite user scripts repository](https://github.com/xarantolus/bromite-userscripts/).

### Using your own filter lists
This program is designed in a way that allows easily adding new lists. 

To create a new list:

1. Fork this repository
2. Enable GitHub Actions by switching to the "Actions" tab of your repo, then confirming that you want to enable them
3. Choose a name for the list, e.g. in the following the name is `example-list`
4. Search for filter lists you want to use. You can for example find them [here](https://filterlists.com/), use those in "uBlock Origin" or "AdBlock Plus" format (however, it's possible that [not all types of rules are supported](https://github.com/bromite/bromite/wiki/AdBlocking)). Go to info, then "View" and copy the URL to the list.
5. Create a file `lists/example-list.txt` (aka in the `lists` directory) that contains the URLs to filter lists you copied before. It should look like this:
    ```
    # Lines starting with # are ignored, empty lines are also allowed
    # List one URL per line:
    https://easylist.to/easylist/easylist.txt
    https://...

    # The following line doesn't work, only put either a comment or an URL in one line, not both
    http://  # Invalid comment on URL
    ```
6. Save your file, commit and push. GitHub actions should now build the list and create a release
7. After GitHub Actions generated the release, you can copy the linked URL in the release to always get the latest generated version. This URL looks something like `https://github.com/USERNAME/filtrite/releases/latest/download/FILENAME.dat`. 
8. Check that the generated filter file size is less than the allowed maximum of [10 MB](https://github.com/bromite/bromite/blob/e5771ef891cf01dd5aeaaec5e092841929a9a541/build/patches/Bromite-AdBlockUpdaterService.patch#L1152-L1153). If it isn't, you must remove some lists
9. Set this URL as the filter file in Bromite settings.

Another thing to note is that [GitHub disables scheduled workflows after 60 days](https://docs.github.com/en/actions/managing-workflow-runs/disabling-and-enabling-a-workflow), meaning that you sometimes have to commit something to keep your fork "alive".


### [License](LICENSE)
This is free as in freedom software. Do whatever you like with it.
