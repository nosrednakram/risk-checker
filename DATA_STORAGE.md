## Data Storage Systems

The biggest issue will be the volume at specific times of the day. The issues will arise when we experience blocking and generating data sources etc. Archiving and guaranteed storage before looking up results will be required without causing the underlying system to bog down with queries and data writes. To avoid this I propose using several different storage systems based on the task being performed with a consolidated record storing the results. 

We will need a scalable storage solution. I propose we design with dependency inversion so we can easily change out the storage solutions as requirements evolve. I'm liking Redis which on modist hardware can handle close to 700,000 push/pop actions a second, for our record format, or close to 400,000,0000 over ten minutes. Setting up a FIFO queue on Redis will allow us to move that data to more permanent storage overtime to balance out the load requirements. 

Depending on the database(s) to be used we will pop from our FIFO queue and add to permanent storage. We have a few heavy correlation tasks to manage. 

  * Contact Risk Level based on proximity to:
    * People
    * Places
    * Events
  * Daily evaluation, and scoring?
  * Who needs to be warned due to their assessed risk.
  * Rolling risk scores
    * Use a period as a starting point
      * Assess if risk increased/decreased over the prior period 
  * ...

I believe any calculation that requires a heavy process should evaluate and determine the best storage solution for the task and the data should be maintained in that format for the task. We can also limit "locks" by scheduling batch data loads between tasks. All results should be stored in the primary database which will have an overview of the QRCodes risk factors. 

This application will have many data-intensive tasks to be efficient we will store the results of these risk factors in a consolidated user record and assess risk using Fuzzy logic. This will allow us to do a very quick analysis
of risk so we can offer near real-time feedback based on many resource-intensive calculations. We can also use old data to train the system. Additional metrics will also be added removed as we learn more. 

Systems should be purged of unneeded data when possible. We don't want to lose data so we will need to archive it.   At this point, the data will still be valuable for research. To that end, we will need to archive the data to be consumed by researchers on their/our research systems. 
Flat file delimited or positional solutions will be used and the old data purged for the active system(s). The goal is to not waste data but keep the realtime system's data minimized for the efficiency of calculations. 
