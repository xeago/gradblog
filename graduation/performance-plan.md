---
layout: simple
title: Performance plan
---

This document defines how I intend to prove my competencies. These competencies are described in the [Education and Examination Regulations]. Competencies are measured according to Performance Indicators.  
This document will be used during the assessment as source for the competencies to be proven.

---

# Listing of performance indicators
This listing is freely translated by the author. When in doubt or in event of conflict with the [original Dutch version][DutchPI], the latter will prevail.

<ol>
<li id="PI01" value="1">A student demonstrates in practice that the (SE) instruments (method / technique) have been effectively used.</li>
<li id="PI02" value="2">A student demonstrates in practice on the basis of valid arguments to have taken a grounded (design) decision.</li>
<li id="PI03" value="3">A student delivers a product, result that meets the agreed requirements and quality.</li>
<li id="PI04" value="4">A student demonstrates that a product has been adequately validated.</li>
<li id="PI05" value="5">A student reports formally and adequately of the result and the progress of work.</li>
<li id="PI06" value="6">A student gives a business grounded, robust advice.</li>
<li id="PI07" value="7">A student formulates a program of requirements for the product to be delivered to the satisfaction of the stakeholders.</li>
<li id="PI08" value="8">A student develops a SMART-plan considering the requirements for a product to be delivered or work to be carried out.</li>
<li id="PI09" value="9">A student provides a logical, clear, feasible, manageable work breakdown structure for a complex task, assignment.</li>
<li id="PI10" value="10">A student shows in the SE field to be able of making an adequate analysis and model of a complex problem as assessed by stakeholders.</li>
<li id="PI11" value="11">A student communicates in a pleasant and effective manner with each other and with stakeholders.</li>
<li id="PI12" value="12">A student demonstrates in practice to be able to discuss in a result-oriented dialogue.</li>
<li id="PI13" value="13">A student demonstrates to carry out a project in a controlled manner, according to plan.</li>
<li id="PI14" value="14">A student gives an adequate view of the progress and results of the work to create a bigger basis of understanding.</li>
<li id="PI15" value="15">A student demonstrates in practice to be able to make a conceptual integer design.</li>
<li id="PI16" value="16">A student demonstrates in practice to be able to realize an integer design.</li>
<li id="PI17" value="17">A student demonstrates in practice his professional attitude (loyalty, honest, flexible, ..).</li>
<li id="PI18" value="18">A student demonstrates in practice to have used all available information sources effectively and efficiently for the stated objective.</li>
<li id="PI19" value="19">A student demonstrates in practice to be able to deliver effective documentation.</li>
<li id="PI20" value="20">A student demonstrates in practice to implement a result in a systematic manner.</li>
<li id="PI21" value="21">A student demonstrates in practice to perform corrective, perfective, adaptive maintenance and management.</li>
<li id="PI22" value="22">A student demonstrates in practice to have learned of work, mistakes.</li>
</ol>

# Chosen performance indicators

  |         |                                                                                       
-:|:-------:|-----------|
PI          | [1][PI01] | A student demonstrates in practice that the (SE) instruments (method / technique) have been effectively used.
Description |           | Understanding and the ability to use suitable methods and techniques are key to a professional software engineer.
Relevance   | 4         | 
Instruments |           | Jekyll, tire & elasticsearch, capistrano, puppet, ssh, git, MVC and more.
Reflection  | ++        | I had fun in my spare time looking at a lot of these tools. I chose to use Jekyll for maintaining my blog aswell as a document typesetting for all my graduation documentation. I learned how to use puppet by using it to bootstrap new installations of OS X for future laptops. Puppet works over ssh, which I was already familiar with (ssh allows you to remotely control another computer). I was then able to use this knowledge for use in bootstrapping virtual machines (on AWS) for my tests. I use git for source control because in my opinion it is the best that is available, VideofyMe uses it too. I put almost everything into source control! Several design patterns have been used appropriately in the codebase. This made it even easier to implement since part of the structure was already well known.
Products    |           | (description of the) usage of relevant instruments (see above).


  |         |                                                                                       
-:|:-------:|-----------|
PI          | [2][PI02] | A student demonstrates in practice on the basis of valid arguments to have taken a grounded (design) decision.
Description |           | Within the design of software, the system architecture and the system deployment process, decisions with their arguments will be documented.
Relevance   | 3         | During my orientating internship I was criticized for hesitating to make decisions. I wish to improve on this aspect.
Reflection  | ++        | Based on gathered test results, I proposed a setup that was then also chosen by my supervisor after understanding my reasoning. While he finalized the decision (as he is in charge of keeping the system operational), it would have been my decision too.
Products    |           | [Test results] accompanied by my [musings] about the subject.

  |         |                                                                                       
-:|:-------:|-----------|
PI          | [3][PI03] | A student delivers a product, result that meets the agreed requirements and quality.
Description |           | An approved acceptance test will take place. Part(s) of this plan measures compliance with the agreed requirements and quality.
Relevance   | 5         | I want to be evaluated on the result of my internship. Being able to deliver results is key to a professional software engineer.
Reflection  | -         | I did not do this as formally as I wanted, but in my opinion the effect remains the same: assert the quality and acceptance of delivered products. I did this using a short questionnaire, also answered by my supervisor (for good measure: he answered positive on all questions).
Products    |           | A [questionnaire] served as an acceptance test for the requirements described in my [graduation assignment] and [architectural requirements].

[questionnaire]: architecture/infrastructure/questionnaire.png

  |         |                                                                                       
-:|:-------:|-----------|
PI          | [4][PI04] | A student demonstrates that a product has been adequately validated.
Description |           | A result for the wrong problem is not the desired result, therefore an approved acceptance test will take place.
Relevance   | 2         | I want to be evaluated on the result of my internship. Being able to deliver the desired result is key to a professional software engineer.
Reflection  |  -        | The system works as requested, this has been asserted using the [questionnaire].
Products    |           | System for searching videos and related documentation.

<div id="ref-PI05" class="ref"></div>

  |         |                                                                                       
-:|:-------:|-----------|
PI          | [5][PI05] | A student reports formally and adequately of the result and the progress of work.
Description |           | A fortnightly report on status will be broadcasted. These reports will contain information about my activities and their outcomes.
Relevance   | 1         | Due to my internship being abroad keeping good contact is of high importance.
Reflection  |   0       | I did my best to not forget to publish these reports on time, yet, sometimes this still slipped a bit. However, I haven't heard complaints about missing reports, I hope this did not get noticed and did/does not cause any issues.
Products    |           | Raw e-mail messages (available on request), [status-reports], [memos].

  |         |                                                                                       
-:|:-------:|-----------|
PI          | [6][PI06] | A student gives a business grounded, robust advice.
Description |           | Part of the end-result is the advice for the architecture for elasticsearch nodes. This advice will be backed by several documents providing additional information. The chief technology officer (CTO) of VideofyMe will review this advice and provide feedback which shall serve as verification.
Relevance   | 3         | 
Reflection  |   ++      | After discussing my [musings for the architecture] and the [test results] with my supervisor, he asked what I would do. This then became his decision too.
Products    |           | An advice for the architecture for elasticsearch nodes, based on research. Review of CTO. Both of these were done in person at the office. The documents used during this discussion are linked to in the reflection.

  |         |                                                                                       
-:|:-------:|-----------|
PI          | [10][PI10]| A student shows in the SE field to be able of making an adequate analysis and model of a complex problem as assessed by stakeholders.
Description |           | Part of the end-result is an architecture for elasticsearch nodes. These will be described, analyzed and tested.
Relevance   | 3         | 
Reflection  |   ++      | Based on the requirements and the gathered knowledge about the systems used, an adequate analysis and model have been made. With the aid of this model the test results have been constructed.
Products    |           | Section(s) within advice and research documents: [architecture requirements], [architecture design] and the [test results].

  |         |                                                                                       
-:|:-------:|-----------|
PI          | [11][PI11]| A student communicates in a pleasant and effective manner with each other and with stakeholders.
Description |           | Communication is necessary to transfer findings to the target parties. Information contained will be clear and understandable.
Relevance   | 4         | Due to my internship being abroad keeping good contact is of high importance.
Reflection  |  ++       | The communication with the supervisors were pleasant.
Products    |           | Archive of all textual-communication (available on request), reflection of stakeholders (not yet received, the mid-term [evaluation] is available).

  |         |                                                                                       
-:|:-------:|-----------|
PI          | [14][PI14]| A student gives an adequate view of the progress and results of the work to create a bigger basis of understanding.
Description |           | Supervisors obtain a basis of understanding by getting feedback early and often about the work performed and its results. This feedback contains concise, coherent information.
Relevance   | 4         | 
Reflection  |   0       | I have not received many feedback messages on my status reports or memos. However only a few remarks were made during the video conferences with my supervisor.
Products    |           | Feedback messages, [status-reports], [memos], [portfolio](index.html).

  |         |                                                                                           
-:|:-------:|-----------|
PI          | [15][PI15]| A student demonstrates in practice to be able to make a conceptual integer design.
Description |           | Implementing an integer design should not lead to questions about the design. Prove of this can be established on two ways: successful implementation of the design can be used as prove of a design being integer and a survey of colleagues — knowledgeable in the domain.
Relevance   | 4         | 
Reflection  |   ++      | The design has been implemented completely, it has even been extended without requiring structural change to the design.
Products    |           | Documentation for the design of distributed search architecture (from advice/research documents) and the documentation for the design of search: see the [design] document. [Survey results][questionnaire].

  |         |                                                                                       
-:|:-------:|-----------|
PI          | [16][PI16]| A student demonstrates in practice to be able to realize an integer design.
Description |           | Validated documentation with the implementation is part of the end-result. Backtracking the designs, and the decisions within them will serve as validation of the documentation.
Relevance   | 4         | 
Reflection  |  ++       | No changes to the design were necessary for the implementation of additional components. This proves that the design was proper and properly realized.
Products    |           | Documentation for the design of distributed search architecture (from advice/research documents) and the documentation for the design of search: see the [design] document.

  |         |                                                                                       
-:|:-------:|-----------|
PI          | [17][PI17]| A student demonstrates in practice his professional attitude (loyalty, honest, flexible, ..).
Description |           | Soft skills are important in any project for a pleasant, successful execution. Examples of soft-skills are: cooperativeness, eagerness to learn, self criticism.
Relevance   | 4         | 
Reflection  |  +        | VideofyMe (and employees) have expressed their gratitude to me. They would only do so if I was considered a good employee, thus having the necessary soft-skills.
Products    |           | Reflection of supervisors and colleagues (not yet received, the mid-term [evaluation] is available).

  |         |                                                                                       
-:|:-------:|-----------|
PI          | [18][PI18]| A student demonstrates in practice to have used all available information sources effectively and efficiently for the stated objective.
Description |           | Reliability and verifiability of information are important for the end-result. Information sources will be carefully considered and cited in a bibliography.
Relevance   | 4         | 
Reflection  |    +      | I have contacted the authors in many cases for official documentation or further information regarding a specific topic. With that information I was able to verify other sources. I also received a preview of the official Elasticsearch book (but this is also because I was considered very helpful on IRC and was asked to proof read the book subsequently).
Products    |           | Bibliography, mostly available in the extended abstract.

  |         |                                                                                       
-:|:-------:|-----------|
PI          | [19][PI19]| A student demonstrates in practice to be able to deliver effective documentation.
Description |           | Documentation must serve a clear purpose without distractions and ambiguities.
Relevance   | 4         | Maintaining, extending a distributed architecture is no easy job, it should not be made harder by omitting useful documentation.
Reflection  |    +      | I have kept documents to their sole purpose. For example, I did not bloat documents with my personal opinion but I wrote these down in a seperate document containing only my personal opinion (and occasionally my opinion about someone else's opinion).
Products    |           | Design documents.

  |         |                                                                                       
-:|:-------:|-----------|
PI          | [22][PI22]| A student demonstrates in practice to have learned of work, mistakes.
Description |           | While this internship will conclude with my graduation, learning is a process that never completes. Unfortunately, it is not feasible to log every skill or knowledge that is acquired. To compensate for this, a short reflection-memo will be broadcasted monthly.
Relevance   | 5         | Learning, from any origin, is of utmost importance for any software engineer.
Reflection  |   0       | I learned a lot, from development to system administration to devops; I consider all these extremely valuable. I have documented monthly in my memos and also in my [reflection].
Products    |           | Monthly [memos].

[memos]: memos.html
[test results]: architecture/test-results.html
[musings]: architecture/musings.html
[status-reports]: status-reports.html
[graduation assignment]: graduation-assignment.html
[musings for the architecture]: architecture/musings.html
[architecture requirements]: architecture/requirements.html
[architecture design]: architecture/design.html
[evaluation]: evaluation/supervisor.html
[design]: architecture/design.html

#### References
+ [Dutch performance indicators][DutchPI], page 6: "Algemene Prestatie-indicatoren"
+ [Education and Examination Regulations]

[DutchPI]: http://infonet.hszuyd.nl/files/usr_beumersjpa/Toetsboeken%20I/Toetsboek%20I%20en%20TI%202011-2012.pdf
[Education and Examination Regulations]: http://infonet.hszuyd.nl/files/usr_beumersjpa/Opleidingsregelingen%20I/OER%20I%20en%20TI%202012-2013.pdf
[PI01]: #PI01
[PI02]: #PI02
[PI03]: #PI03
[PI04]: #PI04
[PI05]: #PI05
[PI06]: #PI06
[PI07]: #PI07
[PI08]: #PI08
[PI09]: #PI09
[PI10]: #PI10
[PI11]: #PI11
[PI12]: #PI12
[PI13]: #PI13
[PI14]: #PI14
[PI15]: #PI15
[PI16]: #PI16
[PI17]: #PI17
[PI18]: #PI18
[PI19]: #PI19
[PI20]: #PI20
[PI21]: #PI21
[PI22]: #PI22
