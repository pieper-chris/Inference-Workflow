# Software Requirements Specification
**Inference Workflow**: a business-oriented workflow tracking system

> This document is subject to change
## Contents

<ol type="I">
<li> <a href="#intro">Introduction</a>
  <ol type="a">
  <li> <a href="#purpose">Purpose</a>
  <li> <a href="#doc-conventions">Document Conventions</a>
  <li> <a href="#scope">Scope</a>
  <li> <a href="#references">References</a>
    <ol type="i">
      <li> <a href="#internal">Internal References</a>
      <li> <a href="#external">External References</a>
    </ol>
  </ol>
<li> <a href="#overview">Overview</a>
  <ol type="a">
  <li> <a href="#prod-perspective">Product Perspective</a>
  <li> <a href="#function">Functionalities</a>
  <li> <a href="#users">User Classes and Characteristics</a>
  <li> <a href="#environment">Operating Environment</a>
  <li> <a href="#constraints">Design and Implementaiton Constraints</a>  
  <li> <a href="#assumptions-dep">Assumptions and Dependencies</a>
  </ol>
<li> <a href="#sys-feat">System Features</a>
  <ol type="a">
  <li> <a href="#functional-req">Functional Requirements</a>
  </ol>
<li> <a href="#extern-int">External Interface Requirements</a>
  <ol type="a">
  <li> <a href="#user-ints">User Interfaces</a>
  <li> <a href="#hardware-ints">Hardware Interfaces</a>
  <li> <a href="#software-ints">Software Interfaces</a>
  <li> <a href="#Comm-ints">Communications Interfaces</a>
  </ol>
<li> <a href="#extern-int">Nonfunctional Requirements</a>
  <ol type="a">
  <li> <a href="#perf-reqs">Performance Requirments</a>
  <li> <a href="#safety-reqs">Safety Requirements</a>
  <li> <a href="#sec-reqs">Security Requirments</a>
  <li> <a href="#soft-qa">Software Quality Attributes</a>

</ol>




## <a name="intro">Introduction</a>

### <a name="purpose">Purpose</a>
The goal of this document is to establish a design for the creation of an entire web application that tracks online workflow tickets from opening/creation to close/resolution. Although many such applications already exists, they are never truly one size fits all. This application, "Inference Workflow", will be no different, as it is intended for smaller groups or people working alone. The idea is to keep features simple, while providing an artificial intelligence solution to present informative closure/resolution timing estimates for customers. <a href="#ai_module">**See AI for more details**.</a>


### <a name="scope">Scope</a>

The Inference Workflow web application can provide a simpler alternative to major workflow apps such as ServiceNow. While these apps are phenomenal, they may have too many features for a smaller group or single person. Besides simplicity, Inference Workflow will strive to create a unique time estimate experience for customers that are given reference to their service tickets to monitor progress. This will be done with reinforcement learning methods and similar artificial intelligence concepts. Inference Workflow will follow the standard Model-View-Controller design pattern and make use of a relational database for storage of predefined workflow attributes on a per-ticket basis.

In short, the Inference Workflow system will provide a simple way to track and update work tickets from start to finish. The abstract back-end RL system will then provide the customer with smart completion time estimates based on multiple sources of real-time data. Overall, I hope to provide an easy workflow solution that doesn't require training to understand.

### <a name="doc-conventions">Document Conventions</a>

```
DB = Database
ER = Entity Relationship
VB = Visual Basic (Microsoft)
AWS = Amazon Web Services
MVC = Model-View-Controller
RL = Reinforcement Learning

```


### <a name="references">References</a>

> #### <a name="internal">Internal References</a>

*  Coming Soon

> #### <a name="external">External References</a>

* Coming Soon

### <a name="overview">Overview</a>

#### <a name="prod-perspective">Product Perspective</a>

> Inference Workflow will store and update the following information in a relational database:

<ol>
<li> Workflow Tickets
  <ul>
    <li> Contains all initial contact information from employee and customer, appropriate title of task, troubleshooting/resolution notes, possible attachments, completion status, and customer feedback after resolution/closure.
  </ul>
<li> Worker Profiles
  <ul>
    <li> Contains basic account and contact information for employee
  </ul>
<li> Global sentiment variable for time estimate computation
  <ul>
    <li> Output of latest external sentiment evaluation
  </ul>
</ol>

#### <a name="function">Functionalities</a>

> The following ER model shows the main database product features

![Error Loading Image](https://github.com/pieper-chris/Inference-Workflow/blob/main/docs/images/InferenceWorkflowSRS-2.png)


#### <a name="users">User Classes and Characteristics</a>

> Inference Workflow should allow users to create, update, and view service tickets that are stored in the database. The application will support both employee/worker privileges and external/customer views.

Employees/Workers will have the following functionalities available:

<ul>
  <li> Full login and home dashboard for current workflow status
  <li> Administrative tools
    <ul>
      <li> Create/edit tickets (no deletion for logging purposes)
      <li> Add notes and useful info to assist in resolution/closure
      <li> Add notes and useful info to assist in resolution
      <li> Update completion status for assigned tickets
    </ul>
  <li> Customer functions
  <ul>
    <li> View all tickets in personal queue to resolve/close
    <li> Get all customer feedback from previously assigned tickets with closed/resolved status
    <li> Get all previously assigned tickets for reference
    <li> Send update and/or resolution emails to customer through the specific ticket view
  </ul>
</ul>

Customers will have the following functionalities available:

<ul>
  <li> External viewing of ticket status
  <ul>
    <li> Search for ticket status by ticket ID given by assigned worker
    <li> View select status information including a RL completion estimate
  </ul>
</ul>

#### <a name="environment">Operating Environment</a>

The operating environment for this web application is as follows:

<ul>
  <li> Operating system: any with access to popular browsers
  <li> Platform: <a href="https://visualstudio.microsoft.com"> .NET (ASP.NET MVC) in Visual Studio - C# Language </a>
  <li> Hosting: <a href="https://aws.amazon.com/?nc2=h_lg"> AWS </a>
  <li> Database: <a href="https://www.microsoft.com/en-us/sql-server/sql-server-downloads">SQL Server 2019 Express</a>
  <li> Client/Server System
  <li> Design: free/public <a href="https://startbootstrap.com/theme/sb-admin-2" >bootstrap template </a>
</ul>

#### <a name="constraints">Design and Implementaiton Constraints</a>  

<ul>
  <li> SQL commands for the functionalities mentioned above
</ul>

#### <a name="assumptions-dep">Assumptions and Dependencies</a>

As a workflow ticketing system, the following main actions will occur:

1. A ticket will be created by the employee for every customer and issue that is necessary.
2. Each ticket will be worked through to completion or closure
3. Inference-based estimates will be applied with RL for each open ticket until closure/resolution.

With such actions successfully being carried out, Inference Workflow has been designed as a database for employees to resolve customer tickets.


## <a name="sys-feat">System Features</a>
The workflow ticketing system maintains individual ticket information for better productivity and/or troubleshooting. The reasons for creating a customer ticket can pose a range of different priorities (which is an attribute marked upon creation).

In this case, ease of use and consistency is what matters most. This also allows the RL algorithm to perform more accurately over time.

### <a name="functional-req">Functional Requirements</a>
<ul>
  <li> Ability for employee to create/edit/view any ticket in queue or previously resolved
  <li> Displays dashboard of ticket queue, ticket progress, and more trends for employees who are signed in to the application
  <li> Display select information and agent-estimated ticket completion for customers (externally: no sign-in)
</ul>

## <a name="extern-int">External Interface Requirements</a>

### <a name="user-ints">User Interfaces</a>

* Front-end: VB ASP.NET with free-to-use bootstrap template
* Back-end: SQL Server 2019 Express

### <a name="hardware-ints">Hardware Interfaces</a>

* Any modern, popular web browser

### <a name="software-ints">Software Interfaces</a>

* OS - macOS Big Sur for development
* Implementation Environment - Visual Basic
* Database - SQL Server 2019 Express
* Deployment/Hosting - Amazon Web Services

### <a name="Comm-ints">Communications Interfaces</a>

* Any modern, popular web browser

## <a name="extern-int">Nonfunctional Requirements</a>

### <a name="perf-reqs">Performance Requirments</a>

Coming Soon.

### <a name="safety-reqs">Safety Requirements</a>

Database issues may require falling back to archived storage. More on this with time...



### <a name="sec-reqs">Security Requirments</a>

Coming Soon.

### <a name="soft-qa">Software Quality Attributes</a>

Coming Soon.

----


## <a name="ai_module"> Artificial intelligence Module </a>

In my time working as a IT service desk specialist, I noticed a pattern of customers calling in to get status updates on their problem tickets. After looking through these tickets and contacting the IT worker assigned to it, my answer would often be unsatisfying to give. Simply put, there are too many factors to know for sure, particularly in a large business that reaches many different types of end users.

One possibly useful solution is to utilize Artificial Intelligence to give the end user an on-demand estimate on the timing of their ticket's closure. This AI agent would make use of data from the outside world (current news, markets, etc.) along with input from those working on the ticket assigned to them. After weighing the inputs appropriately, the end-user can get a reasonable idea of the timing trend in which their ticket is to take.

 We know that daily events outside of the workplace can affect productivity whether we want it to or not. Although we can do a good job as individuals to avoid distraction, major events (positive or negative) can disrupt the workday by means of security precautions or stress-induced lack of productivity. To remove bias and potential stress for the worker using this app, the outside data trends would be hidden from the dashboard by default, but this can be changed if that is not the ideal way to address this.
