# Programming-Framework-Assessment
Write a pseudocode that processes each application as an input in JSON form into an output page with basic information, eligible banners, and scores table.
## Basic Information Provided

Below is the pseudocode for rendering the basic information

```
/*
Note:
- 0th index
- `${variable} string` for string format
/*

// class for complicate objects (e.g. education, experience)
create Class(es) with methods
- createString() to create a string in a certain format 
- getSortVal() to get value for sorting with other instances in the same class


create an object (referred as basicObj) for basic info part 
- key -> text to be shown
- value -> a collection of 
    - corresponding value
    - rendering option 
    - (optional) add. params depending on rendering option
- ex. {"Name": 
          [
            `${input['fisrtName']} ${input['lastName']}`, // corresponding value
            "identity" // rendering option
          ],
       "Most recent education": 
          [ 
            input['educations'], // corresponding value
            "latest", // rendering option
            "education" // Class name for rendering option
          ]
       }

// start rendering basic info
basicTxtLst = [] // store lines for basic info
for key, lst in basicObj

    val = lst[0] // corresponding value
    option = lst[1] // rendering option 

    if option is "identity"
        add `<b>${key}:</b> ${val}` to basicTxtLst

    else if option is "latest"
        className = lst[2]
        create an instance of Class with className for each element in val
        descendingly sort instances by instance.getSortVal()
        add sortedInstances[0].createString() to basicTxtLst

join lines in basicTxtLst by line break char
```
## Tasks
1. Evaluate this pseudocode. What is good and why? What is bad and why? How could this pseudocode be improved?

**Answer**

What is good and why?

The good part about this pseudocode is that it provides basic understanding of the scenario. The code has defined the classes and methods separately and it also defines how it will render through the list. 

What is bad and why?

The bad part about this pseudocode is that the elseif condition for the "latest" rendering option will not be met in any case if the conditions above it are met.

How could this pseudocode be improved?

Replace the elseif condition with an if condition so that all the required rendering options are checked before producing an output. 

2. Revise this pseudocode (feel free to change its structure as you see fit) to match the hiring managers' new requests. The hiring managers change their minds and now want:
- the applicant's native languages to be displayed
- all of the experiences to be displayed in descending order instead of just the most recent one (still keep displaying only most recent education)

**Answer**

- the applicant's native languages to be displayed



- all of the experiences to be displayed in descending order instead of just the most recent one (still keep displaying only most recent education)


3. Now it is your turn to come up with the pseudocode! Choose either Eligible Banners or Scores Table part to work on. The pseudocode you write can be at the algorithm/framework level.
   - consumes the JSON input
   - processes information from the consumed input
   - constructs the page output
  
**Answer**

I have chosen Eligible Banners to work on. The below is the pseudocode.  

```

Note:
- 0th index
- `${variable} string` for string format
/*

// class for complicate objects (e.g. education, experience)
create Class(es) with methods
- createString() to create a string in a certain format
- getSortVal() to get value for sorting with other instances in the same class

  ========================================    
Solution class:
Class Banner
This class contains 8 Methods added
- checkGenderSexOrientationForBanner() returns varGenderSexOrientation (boolean)
  - Logic summary: This method will check the diversityInfo for (gender is not Cisgender) or (sex is Other/Intersex) or (sexualOrientation is not Heterosexual)

- checkDisablilityForBanner() return boolean varDisablilityForBanner (boolean)
  - Logic summary: This method will check if there is any disablity

- checkRaceForBanner() return boolean varRaceForBanner (boolean)
  - Logic summary: This method will check if (race contains any of American Indian or Alaska Native and Native Hawaiian or Other Pacific Islander)

- getDiversityCampaignBannerName(varGenderSexOrientation, varDisablilityForBanner, varRaceForBanner) returns bannerName 
  - Logic summary: This method will return the bannerName if any of the above checks are true

- checkEntryLevelEmployEligibilityAndGetBannerName() returns bannerName
    - Logic summary: This method will check if the applicant is eligible for this program if the total length of prior experiences with employmentType as Full-time is no longer than a year

- checkEnglishScoreEligibilityAndGetBannerName() return  bannerName
    - Logic summary: This method will check if the applicant is eligible for this handicap if nativeLanguages doesn't contain EN

- getBannerName() // This method calls all above the methods and gets Banner Name depending on the diversityInfo

- getBannerLinkForProvidedBannerName(bannerName) // This method gets the link to an internal SCM page for the Banner containing more information for hiring managers to click
  ========================================    
create an object (referred as basicObj) for basic info part
- key -> text to be shown
- value -> a collection of
    - corresponding value
    - rendering option
    - (optional) add. params depending on rendering option
- ex. {"Name":
          [
            `${input['fisrtName']} ${input['lastName']}`, // corresponding value
            "identity" // rendering option
          ],
       "Most recent education":
          [
            input['educations'], // corresponding value
            "latest", // rendering option
            "education" // Class name for rendering option
          ]
       }
  ========================================    
Solution object:
{
    "Basic Information": {
        "Name":
         [
            `${input['fisrtName']} ${input['lastName']}`,
            "identity" // rendering option
         ],
         "Age":
         [
            input['age'],
            "identity2" // rendering option
         ]
        "Most recent education":
          [
            input['educations'], // corresponding value
            "latest", // rendering option
            "education" // Class name for rendering option
          ],
         "Most recent experience":
          [
            input['experiences'], // corresponding value
            "latest", // rendering option
            "experience" // Class name for rendering option
          ]
    },
    "Banners": {
        "Diversity info":[
            input['diversityInfo'],          
            condition // rendering option
            "banner" // Class name for rendering option
        ],

    }
  ========================================    
// start rendering basic info
basicTxtLst = [] // store lines for basic info
for key, lst in basicObj

    val = lst[0] // corresponding value
    option = lst[1] // rendering option

    if option is "identity"
        add `<b>${key}:</b> ${val}` to basicTxtLst
   
    if option is "identity2"
        add `<b>${key}:</b> ${val}` to basicTxtLst

    if option is "latest"
        className = lst[2]
        create an instance of Class with className for each element in val
        descendingly sort instances by instance.getSortVal()
        add sortedInstances[0].createString() to basicTxtLst

  ========================================    
  Solution added rendering option:
    if option is "condition"
        className = lst[2]
        create an instance of Banner class with className for each element in val
        Get Banner name using instance.getBannerName()
        If bannerName not empty, add bannerName to basicTxtLst // BannerName
        If bannerName not empty, add instance.getBannerLinkForProvidedBannerName(bannerName) to basicTxtLst // BannerUrl
  ========================================    

```

The above pusedocode is desinged keeping maintainbility in mind and it is easy to add, change, or repackage for new purposes. 

Potential scenarios that can happen in the future. 
1. New eligibility banners need to be added. 

In this scenario, it is very simple to update this psuedocode with a new banner method. 

2. Eligibility criteria can change.

In this scenario, the conditions needs to be udpated with regards to the new eligibility changes. 

3. 
