# Database Optimizations

## Observations

**Record the amount of time it takes for the seeds to run.**

Completed running in 1805.816368 seconds.


**Determine how long it takes the index page to load. Record that time.**

45.64 s
59.704 ms Loading
68.570 ms Scripting
118.340 ms Rendering
32.983 ms Other
45.36 s Idle


**Record how long it takes to run the migrations that add indices:**

AddIndices: migrated (0.0025s)
AddMoreIndices: migrated (0.0738s)
AddThirdIndex: migrated (0.3493s)
AddFourthIndex: migrated (5.9449s)


**Use Chrome's developer tools to determine how long it takes the index page to load. Record that time.**

2.61 s

82.737 ms Loading

137.461 ms Scripting

173.424 ms Rendering

15.425 ms Painting

109.061 ms Other

2.09 s Idle


**Calculate your percent improvement in runtime.**

45.64 s to 2.61 s = 94.28%


**Examine the code that is run when the root path loads. Modify the commands which access the database to make them more efficient.**

1.34 s

74.644 ms Loading

77.671 ms Scripting

211.085 ms Rendering

13.562 ms Painting

59.614 ms Other

902.237 ms Idle


**Calculate your percent improvement in runtime.**

2.61 s to 1.34 s = 48.66%

45.64 s to 1.34 s = 97.06%


**Drop the database, run rake db:migrate, and then time how long it takes to run rake db:seed.**

Completed running in 1979.639423 seconds.

**Was there an improvement or a worsening of runtime? By what percent and why?**

Original time to run db:seed: 1805.816368 vs 1975.639423 = 9.4% decrease in speed


Running db:seed takes a little bit longer now that we're adding extra indices


**Which is faster: (a) running rake db:seed without indices and then running a migration to add indices, or (b) adding indices during your initial rake db:migrate, then running rake db:seed?**

Running db:seed without indices then running migrations:
1805.816368+0.0025+0.0738+0.3493+5.9449=1812.186868 s _<- this is faster_

Running db:seed with indices: 1979.639423 s

**Record the size of your database:**

Database size: 569843712

**Record the size of your development log.**

Log size: 1468763493

**Give at least one method (feel free to Google) for reducing the size of one of these, yet keeping your data intact.**

Limit the size of the database:
- Redundant or unused fields can be removed (unlikely to have too many of these in a freshly generated database, I assume?)
-Compression: reduces size of database, possibly at a performance cost, though

Limit the size of the log file:
- In config, logs can be set to rotate once they reach some arbitrary size.

**Do you think that this is smaller, about right, or larger than the size of databases you'll be working with in your career?**

I am reasonably sure that we work with larger databases at Spoonflower (although undoubtedly, some places of employment work with much larger databases still).
