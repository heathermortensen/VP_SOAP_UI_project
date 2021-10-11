# VP_Project

## **Exercise:**

Create an automation project using Python, C#, Java or Kotlin that has both web and api test cases. The project should be in Github and available to VP interviewers to review before the technical interview.

The candidate will use [Pet Swagger](https://petstore.swagger.io) and automate the following requirements:

Requirements:
* Create a new pet and add a picture to it
* Search for new pet and similar pets
* Validate the user can expand and collapse the rest method sections that provide endpoint information on the website

## **Exercise interpretation #1.**

Create a Django (python based) web application named petstoreProjectForVP. Start a new app called heathersPetstoreProject. (Project location: C:\XXX\GitProjectForVirginPulse)

Django was used because: 

1. It takes very little time to standup a web application.
2. It has a REST framework that integrates with Swagger.
3. It has it's own web test framework for automated testing. 

However, reference #4 in figure 1 states that problematic “hiccups” present themselves when you integrate Swagger/OpenAPI and REST API Djano projects. These are summarized in figure 2. I installed the software versions listed in Figure 3.

Reference # | Link |
------------ | --------------|
1 | [Django REST Framework Quickstart](https://www.django-rest-framework.org/tutorial/quickstart/) | 
2 | [Django REST Swagger](https://django-rest-swagger.readthedocs.io/en/latest/) |
3 | [Django Tutorial Part 10: Testing a Django web application](https://developer.mozilla.org/en-US/docs/Learn/Server-side/Django/Testing) |
4 | [Add Swagger to Django Rest API quickly (4 mins) without Hiccups - Cautionary Tale and Solution](https://www.jasonmars.org/2020/04/22/add-swagger-to-django-rest-api-quickly-4-mins-without-hiccups/) |
5 | [SWAGGER_SETTINGS - A dictionary containing all configuration of django-rest-swagger.](https://django-rest-swagger.readthedocs.io/en/stable-0.3.x/settings.html) |
6 | [Django REST Swagger: deprecated (2019-06-04)](https://pythonrepo.com/repo/marcgibbons-django-rest-swagger-python-documentation) | 

**Figure 1. Table of References**

Software | Version |
------------ | --------------|
Django | >=3.0.3,<3.1.0 |
djangorestframework | >=3.11.0, <3.12.0 |
django-rest-swagger | >=2.2.0, <2.3.0 |

**Figure 2. Integrations that go bad** (reference 4)

Software | Version on my PC | Current version | Inside my virtual environment at C:\XXX\myPetstoreProjectForVP | Inside my virtual environment at C:\XXX\petstoreProjectForVP |
------------ | --------------|------------ | --------------|------------ | 
Python | 3.9.7 | 3.9.7 (Aug. 30, 2021) | 3.8 | 3.9.7 | 
Django | 3.1.7 | 3.2.8 | 3.0 | 3.0.11 | 
[Djangorestframework***](https://www.django-rest-framework.org/community/3.11-announcement/#:~:text=Validator%20%2F%20Default%20Context-,Django%20REST%20framework%203.11,2.1%2C%202.2%2C%20and%203.0) | n/a |3.11**| 3.11 | 3.11 | 
[Django-rest-swagger](https://django-rest-swagger.readthedocs.io/en/stable-0.3.x/) | n/a | 2 (2019 deprecated)* | 2.2.0 |------------ | 

**Figure 3. Software versions utilized in this project**

*Swagger version 2.0 is fundamentally different from previous versions and leverages the new schema generation features introduced in [Django REST Framework 3.4](https://django-rest-swagger.readthedocs.io/en/latest)

**constrained by swagger v2 to Django Rest Framework v3.4. Deprecated swagger requirements: Django 1.8+, Django REST framework 3.5.1+, Python 2.7, 3.5, 3.6


***REST framework requires the following: Python (3.5, 3.6, 3.7, 3.8, 3.9) and Django (2.2, 3.0, 3.1, 3.2)

## **Exercise interpretation #2**

REINTERPRETATION of the problem...Maybe I'm not supposed to build a web application. This is test and/or data driven development. 
Build all functional and API tests first. Simply use SoapUI, ReadyAPI, and swagger?

#### Test the API……how? See this: [Functional Tests in ReadyAPI](https://support.smartbear.com/readyapi/docs/functional/creating.html)
---------------------------------------------------------------------------------------------------------------------------------------
* First, I exported the swagger API definition. Filename: `api-docs.json`

```JSON
["Json", "{"swagger":"2.0","info":{"version":"1.0","title":"Swagger Petstore"},"basePath":"petstore.swagger.io/v2","paths":{"/v2/pet":{"post":{"operationId":"/pet","consumes":["application/json","application/xml"],"parameters":[{"in":"body","name":"body","description":"Request body","required":true}],"responses":{"405":{}}},"put":{"operationId":"/pet","consumes":["application/json","application/xml"],"parameters":[{"in":"body","name":"body","description":"Request body","required":true}],"responses":{"400":{},"404":{},"405":{}}}},"/v2/pet/findByStatus":{"get":{"operationId":"/pet/findByStatus","parameters":[{"name":"status","in":"query","description":"Status values that need to be considered for filter","required":true,"type":"string"},{"name":"status","in":"query","description":"Status values that need to be considered for filter","required":true,"type":"string"}],"responses":{"200":{},"400":{}}}},"/v2/pet/findByTags":{"get":{"operationId":"/pet/findByTags","parameters":[{"name":"tags","in":"query","description":"Tags to filter by","required":true,"type":"string"},{"name":"tags","in":"query","description":"Tags to filter by","required":true,"type":"string"}],"responses":{"200":{},"400":{}}}},"/v2/pet/{petId}":{"get":{"operationId":"/pet/{petId}","parameters":[{"name":"petId","in":"path","description":"ID of pet to return","required":true,"type":"string"},{"name":"petId","in":"path","description":"ID of pet to return","required":true,"type":"string"}],"responses":{"200":{},"400":{},"404":{}}},"post":{"operationId":"/pet/{petId}","consumes":["application/x-www-form-urlencoded"],"parameters":[{"name":"petId","in":"path","description":"ID of pet that needs to be updated","required":true,"type":"string"},{"name":"name","in":"query","description":"Updated name of the pet","required":false,"type":"string"},{"name":"status","in":"query","description":"Updated status of the pet","required":false,"type":"string"},{"name":"petId","in":"path","description":"ID of pet that needs to be updated","required":true,"type":"string"},{"name":"name","in":"query","description":"Updated name of the pet","required":false,"type":"string"},{"name":"status","in":"query","description":"Updated status of the pet","required":false,"type":"string"},{"in":"body","name":"body","description":"Request body","required":true}],"responses":{"405":{}}},"delete":{"operationId":"/pet/{petId}","parameters":[{"name":"api_key","in":"header","required":false,"type":"string"},{"name":"petId","in":"path","description":"Pet id to delete","required":true,"type":"string"},{"name":"api_key","in":"header","required":false,"type":"string"},{"name":"petId","in":"path","description":"Pet id to delete","required":true,"type":"string"}],"responses":{"400":{},"404":{}}}},"/v2/pet/{petId}/uploadImage":{"post":{"operationId":"/pet/{petId}/uploadImage","consumes":["multipart/form-data"],"parameters":[{"name":"petId","in":"path","description":"ID of pet to update","required":true,"type":"string"},{"name":"additionalMetadata","in":"query","description":"Additional data to pass to server","required":false,"type":"string"},{"name":"file","in":"query","description":"file to upload","required":false,"type":"string"},{"name":"petId","in":"path","description":"ID of pet to update","required":true,"type":"string"},{"name":"additionalMetadata","in":"query","description":"Additional data to pass to server","required":false,"type":"string"},{"name":"file","in":"query","description":"file to upload","required":false,"type":"string"},{"in":"body","name":"body","description":"Request body","required":true}],"responses":{"200":{}}}},"/v2/store/inventory":{"get":{"operationId":"/store/inventory","parameters":[],"responses":{"200":{}}}},"/v2/store/order":{"post":{"operationId":"/store/order","consumes":["application/json"],"parameters":[{"in":"body","name":"body","description":"Request body","required":true}],"responses":{"200":{},"400":{}}}},"/v2/store/order/{orderId}":{"get":{"operationId":"/store/order/{orderId}","parameters":[{"name":"orderId","in":"path","description":"ID of pet that needs to be fetched","required":true,"type":"string"},{"name":"orderId","in":"path","description":"ID of pet that needs to be fetched","required":true,"type":"string"}],"responses":{"200":{},"400":{},"404":{}}},"delete":{"operationId":"/store/order/{orderId}","parameters":[{"name":"orderId","in":"path","description":"ID of the order that needs to be deleted","required":true,"type":"string"},{"name":"orderId","in":"path","description":"ID of the order that needs to be deleted","required":true,"type":"string"}],"responses":{"400":{},"404":{}}}},"/v2/user":{"post":{"operationId":"/user","consumes":["application/json"],"parameters":[{"in":"body","name":"body","description":"Request body","required":true}]}},"/v2/user/createWithArray":{"post":{"operationId":"/user/createWithArray","consumes":["application/json"],"parameters":[{"in":"body","name":"body","description":"Request body","required":true}]}},"/v2/user/createWithList":{"post":{"operationId":"/user/createWithList","consumes":["application/json"],"parameters":[{"in":"body","name":"body","description":"Request body","required":true}]}},"/v2/user/login":{"get":{"operationId":"/user/login","parameters":[{"name":"username","in":"query","description":"The user name for login","required":true,"type":"string"},{"name":"password","in":"query","description":"The password for login in clear text","required":true,"type":"string"},{"name":"username","in":"query","description":"The user name for login","required":true,"type":"string"},{"name":"password","in":"query","description":"The password for login in clear text","required":true,"type":"string"}],"responses":{"200":{},"400":{}}}},"/v2/user/logout":{"get":{"operationId":"/user/logout","parameters":[]}},"/v2/user/{username}":{"get":{"operationId":"/user/{username}","parameters":[{"name":"username","in":"path","description":"The name that needs to be fetched. Use user1 for testing. ","required":true,"type":"string"},{"name":"username","in":"path","description":"The name that needs to be fetched. Use user1 for testing. ","required":true,"type":"string"}],"responses":{"200":{},"400":{},"404":{}}},"put":{"operationId":"/user/{username}","consumes":["application/json"],"parameters":[{"name":"username","in":"path","description":"name that need to be updated","required":true,"type":"string"},{"name":"username","in":"path","description":"name that need to be updated","required":true,"type":"string"},{"in":"body","name":"body","description":"Request body","required":true}],"responses":{"400":{},"404":{}}},"delete":{"operationId":"/user/{username}","parameters":[{"name":"username","in":"path","description":"The name that needs to be deleted","required":true,"type":"string"},{"name":"username","in":"path","description":"The name that needs to be deleted","required":true,"type":"string"}],"responses":{"400":{},"404":{}}}}}}"]
```


[Swagger](https://swagger.io/docs/specification/about/) is just a format for REST APIs. 
I used ReadyAPI to [export the Swagger API Definition](https://support.smartbear.com/readyapi/docs/apis/export.html). 
"ReadyAPI exports the service definition to the api-docs file." There is a RESTful (blue) and Soap (green) API interfaces in ReadyAPI.
Then, I imported into SoapUI. Soap currently only has RESTful. SoapUI produced 2 files: Petstore_1.wadl and a nicley formated wadl-report.html that might be useful for the final exercise requirement, "Validate the user can expand and collapse the rest method sections that provide endpoint information on the website." Wadl is for SOAP and Swagger is for REST. (min 22 of [webinar](https://www.soapui.org/learn/functional-testing/api-functional-testing-soapui-webinar/))


#### Functional testing……
------------------------------------------------------------------------------------------------------------------------------------
* **Testing Requiement 1: Create a new pet and add a picture to it**

[Test case in SoapUI:](https://www.tutorialspoint.com/soapui/soapui_teststep.htm) "Test_Case_1_Create_pet_and_add_picture" 

1. Test step - "add pet to store"
1. Test step - "add picture to pet"

I made a test suite and Exported results from running the test suite to file [TestSuiteLogExport_10_10_2021_545am.txt](https://github.com/heathermortensen/VP_Project/files/7318014/TestSuiteLogExport_10_10_2021_545am.txt). I was able to create a test case, add some assertions, and add a malfunctioning script (is this done in [Groovy?](https://www.tutorialspoint.com/groovy/groovy_variables.htm)). Some assertions are guaranteed to fail because they equal true if no input is provided.

[Source on REST Testing](https://www.soapui.org/getting-started/rest-testing/)
To Do: \
[ ]   Make this test case better w/ better conditions: 1.) petId is unique in the system, otherwise error. Is the pedId the same in both steps? 2.) Is petId the only required parameter? If its not presnt - error. petId != 0 test. 3.) Test for each combination of null and not null optional parameters. How many combinations? Script some data for that. 4.) Same image is not present more than once in the array. Is this a static or dynamically sized array?  Max size is not exceeded and it cannot fill infinitley with pics.  \

* **Testing Requiement 2: Search for new pet and similar pets**

[Test case in SoapUI:](https://www.soapui.org/docs/functional-testing/properties/working-with-properties/) "Testing_Requirement_2_Search_for_new_pet_and_similar_pets" 

I attempted to play with [data driven functional testing](https://www.soapui.org/docs/data-driven-tests/functional-tests/). However, I had no access to the Data Generator through soapUI's free trial version. I attempted to define Test Step Properties that would maintain a consistent petId parameter = 2 and status = avalible throughout both test steps. I thought properties ought to be defined at the highest level of the test tree to do that. That was not true. I need to look at properties in more depth. 

TEST RESULTS
- At the top level, property petId = 8 is defined and the test fails.
- At the testCase 1 level, it passes. Property set petId = 2.
- Setting petId = 5 at the Properties level seems to have no effect of if the tests pass/fail. 
- At the first test step, my response is no longer displayed, but all assertions pass.
- At the second test step "findPetStatus," the step returns all pets with status = avalible.  

Properties set at the lowest level of the tree might take precedence over peroperties set at the highest levels of the testing tree.

Next, See this video....https://www.soapui.org/learn/functional-testing/api-functional-testing-soapui-webinar/



* What information is contained in the headers?
* Project-1-soapui-project.xml
* Found SSL & certificate. Using OAuth 2
* User creds for logging into server are: tester abc123

To Do: \
[ ]   Upload to GitHub. Email Madelon & notify where repo is.  \
[ ]    API tests \
[ ]    Functional tests  - [Functional Tests in ReadyAPI](https://support.smartbear.com/readyapi/docs/functional/creating.html) \
[x]    [Data Driven Functional Testing video](https://www.soapui.org/docs/data-driven-tests/functional-tests/) \
Had to stop because the free version of SoapUI doesn't allow access to "Data Generator" functionality.
[x]    Functional tests video - https://www.soapui.org/learn/functional-testing/api-functional-testing-soapui-webinar/ \
Soap vs rest costs/benefits: Soap - exacting/ridgid. secure. code first. Lots of complicated relationships defined. Machine readable. Rest - design first. newer and less mature. Best practices that are flexible. Build on tools inherent to the web. Efficient. \
[ ]    Identify the path coverage - saw that in here somewhere \
[ ]    Script a test case using MC/DC \
[ ]    Required tests. draw pic. Dropdown with html file. (github wont accept an html drag and drop \
[ ]    Any valuable info in the windows that are open? \
[x] Export WSDL file from ReadyAPI into SoapUI. Source: [Export to WSDL](https://support.smartbear.com/readyapi/docs/apis/export.html) \
Filename: sample-service_1.wsdl  \
    





