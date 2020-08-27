# Pathfinder Summoner's Scribe

Lovingly forked from https://github.com/qu0zl/pfss

 The Pathfinder Summoner's Scribe (PFSS) can be used to generate on-screen displays or print-outs of summonable creatures from the Pathfinder Role-playing game.

Creatures may be displayed individually, in groups of your choosing, or in pre-populated groups representing useful sets of creatures such as those available through Summon Monster 1, for example

The PFSS will dynamically apply the effects of the Augment Summons feat to any creatures that you wish. Automatically modifying stats such as attacks, skills and even special effect DCs based on this feat. You may apply the feat to some, all, or none of the creatures in a particular list.

## CAVEAT

This version uses some really old (and probably insecure) dependencies.  I do not recommend running this anywhere internet-facing.

## Running PFSS locally in 2020

This project requires Python 2.  If you don't have a Python 2 installation, do that first.

These instructions were put together using Git Bash on a Windows computer.  Your mileage may vary.

### Setup a virtual environment

I don't want the old requirements mixing in with my current development efforts, so I run from a virtual environment
```
pip install virtualenv
virtualenv --python 2 env2
source env2/Scripts/activate
```

### Install dependencies

```
pip install -r requirements.txt
```

### Create local settings

Create a file in the pfss directory called `local_settings.py`
Add a value for the `SECRET_KEY` variable.
The easiest way I found to generate a value for `SECRET_KEY` was to run
```
base64 /dev/urandom | head -c50
```
The contents of `local_settings.py` should look something like this:
```
SECRET_KEY = 'rctFqHaSjOkbrR0y1UACdFGU+7FGxvZmzzvcBjKDihJaB741we'
```

### Setup the local database

Have Django set up the local database and import the necessary data
```
python manage.py migrate
python manage.py loaddata sites
python manage.py loaddata pfss
```
### Rename the site_base.html

The site_base.html template that ships with pinax seems to be found before the copy of site_base.html that we want to use.  I got around this by renaming the file.
The file we need to rename is in `<project directory>/env2/Lib/site-packages/pinax_theme_bootstrap/templates`.  I just renamed mine to NOPEsite_base.html.

### Run runserver

runserver isn't meant for a production environment, but it will serve our needs for running locally.
```
python manage.py runserver
```

### Load the website

Navigate to http://127.0.0.1:8000/pfs/

## Have fun storming the castle!
