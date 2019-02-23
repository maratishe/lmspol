# lmspol
Last Man Standing Proof of Location project

This repo contains 
① mobility traces from [crawdad](http://crawdad.cs.dartmouth.edu) in processed and more easily accessible (Lucene) form, and 
② accelerometer and WiFi scan traces taken on commodity Android smartphones. 

The traces are useful when analysing how one can implement Proof-of-Location 
at wireless network edge.  Early analysis on **traces②** shows that reliable context is difficult to achieve in practice. 
The term **reliable** means that we would like to confert the entire trace (100m walks, etc.) 
into a **hashkey** that would describe a particular location (or trajectory) in an independently verifiable way.

An alternative way is to use **trace①** to model peer-to-peer techniques for Proof-of-Location. 
Since the trace has details GPS traces, one can simulate peers meeting each other and participating in a 
shared calculation procedure that finally leads to a **reliable hashkey**.

