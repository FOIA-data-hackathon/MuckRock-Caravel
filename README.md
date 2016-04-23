<p align="center">
  <img src="http://i.imgur.com/P9IeLIa.png" alt="Muck Rocks!"/>
</p>


# MuckRock-Caravel
> Exploring MuckRock Data in Caravel

This project contains information for creating a data-vis dashboard in [Caravel](https://github.com/airbnb/caravel) that uses MuckRock's request data.

## Converting MuckRock Data

First, you'll need to convert the MR CSV files into a database format that Caravel can understand.

A '[csv2sqlite](https://github.com/rgrp/csv2sqlite)' script is provided in this repo, use it like so:

    $ wget http://muckrock.s3.amazonaws.com/files_static/hackathon/agency.csv
    $ wget http://muckrock.s3.amazonaws.com/files_static/hackathon/requests.csv 
    $ ./csv2sqlite.py agency.csv agency.db adata  
    $ ./csv2sqlite.py requests.csv requests.db rdata # This one is messy but I think that's okay.

## Installing Caravel

Installing Caravel is easy from pip. [This guide](http://airbnb.io/caravel/installation.html) is also handy, but this is the gist of it:

    # Install caravel
    pip install caravel

    # Create an admin user
    fabmanager create-admin --app caravel

    # Initialize the database
    caravel db upgrade

    # Create default roles and permissions
    caravel init

    # Load some data to play with
    caravel load_examples

    # Start the development web server
    caravel runserver -d 

## Loading Our Data

Now, we want to add our data into Caravel. This is a medium pain in the ass, but this [tutorial](http://airbnb.io/caravel/tutorial.html) is sort of useful.

First, [add a new database](http://localhost:8088/databaseview/add) and point it to the SQLite DBs you just made like so, so the path looks something like this (OSX): 

    sqlite:////Users/YOUR_NAME/Projects/MuckRock-Caravel/agency.db

![Import View](http://i.imgur.com/IpoAkgq.png)

Then hit save!

Next, we need to [add the table](http://localhost:8088/tablemodelview/add). Choose your database from the drop down and set the table name. **This is the undocumented but important bit**: The table name MUST match the table name in the DB that we assigned during conversion (either 'adata' or 'rdata', depending on the dataset). If you don't do this, Caravel will totally break and it'll be annoying to fix.

Leave the others as default and hit 'Save'.

![Edit View](http://i.imgur.com/fMTEQa5.png)

Now, go back to the tables list and hit the **edit button** your table. There will be a new tab at the top titled List Table Column. Select the check-boxes for the things that you want to group by (agency names, for instance). Then **save** by going back to the detail tab to hit save (shitty UI).

Now you're ready to explore!

## Playing with the data

Go back to the table view again, but this time click on the name of your table. This will bring you to the explore view. Play around until you make something cool!

To get started doing fun stuff, hit the drop down up top that defaults to 'Table View'. Change this to 'Bubble View' if you want to make a Hans Rosling type bubble chart. Then, get creative!

![The CIA, The NYPD, and the NSA are the most rejecty](http://imgur.com/VUnoZfs)

## Making a Dashboard

![Dash Edit View](http://i.imgur.com/GTEyy3S.png)

When you create a data-viz 'slice' that you like, you can save it for later use in your dashboard. Creating a dashboard is done in the same way that you added tables, just under the dashboard tab. You have to add your slices manually in the form, and then you can arrangement by acutally looking at at the dashboard and dragging them around - just remember to hit save!

Hooray!
