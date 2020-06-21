## Risk Checker 

Themed view: https://nosrednakram.github.io/risk-checker/

Want to be able to do contact tracking without being geo-tagged or having your identity easily shared. I do and based on a conversation recently I woke up with an idea to create a tool to do this easily, assuming public buy-in. In short, the tool will generate QR codes that a user will scan. Upon scanning the user's time and association to the scanned person/place's QR code will be logged. As the users are asked to do a self-assessment each day before using a user's risk can be displayed. A lot more to it but that's our initial idea. 

### Help

This will be my first real go at an open-source project and I'd love all of the help I can get. I feel like I'm new enough to this as to not know what I even need help with. If you like this idea and have skills to offer please reach out. Beyond that, for headings below, I offer what skill I believe would be most helpful. My background covers all areas, with statistics and fuzzy logic being my weakest area.

### Components

The task of doing this will require several servers to isolate performance requirements by the task. With all the options for the virtual systems these days I prefer to design for multiple servers even when developing on a single server.

#### Account Server (Basic Website Front and Back End Developers)

This will be the first server to build and will facilitate:

  * Creating an account
  * Authenticating
    * Setting cookies
  * Resetting password
  * Password recovery
  * Collection of users voluntary meta information
    * Type
     * Person
      * Are you at increased risk
     * Location
      * Safe Capacity
     * Event
      * Safe Capacity
  * Downloading of QR code
  
#### Tracking Server (Back End Servers Developer)

Next up will be the workhorse of the project. It will simply track associations of the systems QR codes.

  * Upon accessing a page store association of user to scanned QR code
  * Display assessed risk 
  
#### Personal Health Assessment (Looking For Health Professional Help)

The goal is to ask a few questions to help identify the risk of the participant having COVID. By asking a few questions a score will be given to the risk the user poses to others. The system will also look at contact tracing to offer another risk assessment. It will then offer suggestions on if the user should self isolate, etc... We will need a balance between the personal self-assessment and the likelihood of exposure based on these systems data to determine overall risk.

#### Proximity Calculator (Fuzzy Logic Anyone) 

This is the math-heavy portion and will and constantly calculate based on activity. e.g. priority to people moving around and making new data points. It will need to be able to assess everyone who has used the system in the last few weeks daily but for those moving around a lot more calculations will have a weighted. This is the second score the Health Assessment system uses when determining overall risk.

#### Storage Server (Systems Storage Experts Welcome)

I have outlined some initial thoughts in another file [DATA_SORAGE](DATA_STORAGE.md). 

#### Communication Server (Systems Communications Expert Welcome(

Simple email/SMS/... services will be passed off and queued up. This will provide account communications and proximity alerts primarily for those not using the system daily if they have a heightened risk of exposure. 

