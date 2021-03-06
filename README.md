# leaguesort

A simple set of utilities to create a sorted leaguetable based on a 
series of results from matches played between the teams.

Takes an input that is a list of results, returning a sorted array
representing the league table based on those results.  The sorted array
can be passed to a templating library or front-end code for display.

The default comparator for a league table is based on the following 
hierarchy; 

Points > Goal Difference > Goals Scrored > Wins > Head2Head

.. but this can be changed by supplying a custom comparator.


## Installation

    npm install leaguesort --save

## Usage

    var leaguesort = require('leaguesort'),
        results = [], 
        table = [];

    results.push({
        homeTeam:'Fuz', 
        awayTeam:'Foo', 
        homeGoals:2, 
        awayGoals:1
    });

    results.push({
        homeTeam:'Bar', 
        awayTeam:'Baz', 
        homeGoals:3, 
        awayGoals:2
    });

    leaguesort.calculateTable(results, table);
    console.log(table);

    // add another result.. cumulative on the same table
    var newResult = {
        homeTeam:'Foo', 
        awayTeam:'Bar', 
        homeGoals:2, 
        awayGoals:2
    };

    leaguesort.calculateTable([newResult], table);

    // change to 2 points per win (default == 3)
    table = [];
    leaguesort.options({winPoints: 2});
    leaguesort.calculateTable(results, table);
    
    // use a non-default comparator to sort the table
    table = [];
    leaguesort.calculateTable(results, table, function(a, b) {
        // alphabetical only
        return (a.name > b.name);
    });


## ToDo

- Enable property mapping for the stats so that callers are not forced
  to use the same input convention

- Create runtime comparators based on desired ordering (i.e. allow a
  runtime configuration that selects "points > goal-diff > head2head"

