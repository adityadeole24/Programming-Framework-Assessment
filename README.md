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

The good part about this pseudocode is that it provides basic understanding of the scenario. The code structure defines the classes and methods separately and it also defines the basic rendering struture. 

What is bad and why?

- The code checks else if condition which is incorrect. This condition will not be checked if the first condition is true. In this scenario we need to display the applicant's name along with the Banner values and scores.
- This psuedocode is missing error handling. The code assumes various aspects of the applicant for e.g. firstname always exist and is correctly formatted.
- This code also has insufficient comments.
  
How could this pseudocode be improved?

- Change all the else if conditions with if conditions to ensure all the conditions are being checked to produce appropriate outcome. 
- Adding error handling will make the code more powerful.
- Adding comprehensive explainations will provide clear information for understanding each part of the code. 

2. Revise this pseudocode (feel free to change its structure as you see fit) to match the hiring managers' new requests. The hiring managers change their minds and now want:
i) the applicant's native languages to be displayed
ii) all of the experiences to be displayed in descending order instead of just the most recent one (still keep displaying only most recent education)

**Answer**

i) the applicant's native languages to be displayed

The psuedocode is updated as below. 
- The "Native Languages" section is added to basicObj with a rendering option for list.
- A comma seprated language list is appended to the basicTxtLst.  

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
- 

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
       "Native Language":
        [
            input['nativeLanguages'], //corresponding value      
            "list", // rendering option
            "language" // Class name for rendering option
        ]   
       }

// start rendering basic info
basicTxtLst = [] // store lines for basic info
for key, lst in basicObj

    val = lst[0] // corresponding value
    option = lst[1] // rendering option 

    if option is "identity"
        add `<b>${key}:</b> ${val}` to basicTxtLst

    if option is "latest"
        className = lst[2]
        create an instance of Class with className for each element in val
        descendingly sort instances by instance.getSortVal()
        add sortedInstances[0].createString() to basicTxtLst

    if option is "list"
       className = lst[3]
       Assign a value to language and a comma seprated list
       add `<b>${key}:,</b> ${list}` to basicTxtLst

      

join lines in basicTxtLst by line break char

```

ii) all of the experiences to be displayed in descending order instead of just the most recent one (still keep displaying only most recent education)

The psuedocode is updated as below. 
- A new rendering option called "descending" is added.
- When rendering experiences with the "descending" option, all experiences are sorted by their startDate in descending order, and each experience is added to basicTxtLst.

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
- 

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
       "Experience in descending order":
        [
            input['experiences'], //corresponding value      
            "descending", // rendering option
            "experience" // Class name for rendering option
        ]   
       }

// start rendering basic info
basicTxtLst = [] // store lines for basic info
for key, lst in basicObj

    val = lst[0] // corresponding value
    option = lst[1] // rendering option 

    if option is "identity"
        add `<b>${key}:</b> ${val}` to basicTxtLst

    if option is "latest"
        className = lst[2]
        create an instance of Class with className for each element in val
        descendingly sort instances by instance.getSortVal()
        add sortedInstances[0].createString() to basicTxtLst

    if option is "descending"
       className = lst[3]
       create an instance of Class with className for each element in val
       Sort experiences by start date in descending order
       add sortedInstances[0].createString() to basicTxtLst
       
join lines in basicTxtLst by line break char

```

3. Now it is your turn to come up with the pseudocode! Choose either Eligible Banners or Scores Table part to work on. The pseudocode you write can be at the algorithm/framework level.
   - consumes the JSON input
   - processes information from the consumed input
   - constructs the page output
  
**Answer**

I have chosen Eligible Banners to work on. The below is the pseudocode. 

```  
//Solution class
Class banner
//This class contains 8 Methods added
- checkGenderSexOrientationForBanner() returns varGenderSexOrientation (boolean)
//Logic summary: This method will check the diversityInfo for (gender is not Cisgender) or (sex is Other/Intersex) or (sexualOrientation is not Heterosexual)

- checkDisablilityForBanner() return boolean varDisablilityForBanner (boolean)
//Logic summary: This method will check if there is any disablity

- checkRaceForBanner() return boolean varRaceForBanner (boolean)
//Logic summary: This method will check if (race contains any of American Indian or Alaska Native and Native Hawaiian or Other Pacific Islander)

- getDiversityCampaignBannerName(varGenderSexOrientation, varDisablilityForBanner, varRaceForBanner) returns bannerName 
//Logic summary: This method will return the bannerName if any of the above checks are true

- checkEntryLevelEmployEligibilityAndGetBannerName() returns bannerName
//Logic summary: This method will check if the applicant is eligible for this program if the total length of prior experiences with employmentType as Full-time is no longer than a year

- checkEnglishScoreEligibilityAndGetBannerName() return  bannerName
//Logic summary: This method will check if the applicant is eligible for this handicap if nativeLanguages doesn not contain EN

- getBannerName() 
// Logic summary: This method calls all above the methods and gets Banner Name depending on the diversityInfo

- getBannerLinkForProvidedBannerName(bannerName) 
// Logic Summary: This method gets the link to an internal SCM page for the Banner containing more information for hiring managers to click
  
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
  Solution rendering option:
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

