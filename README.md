### GENICS docs

## Updating these docs

All changes are made within *docs/source*. For example, the issues page lives within *issue/index.rst*.
these file are a lot like markup and the syntax is really easy to pickup. Documentation exists 
[here](https://www.sphinx-doc.org/en/master/).


Simply run *make html* in the *docs* directory to create the html. Then, in the root directory open *index.html* to
go to the main page. 


Everytime you need to create a new page, you must update *source/index.rst* with the path (e.g., search for set_up_env/index.rst in that file)


Simply commit and push the changes to master and then they will be live [here](https://pmgates42.github.io/GENICS-docs.github.io) after the site
is recompiled.
