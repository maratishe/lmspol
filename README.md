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


# crawdad traces 

The raw data comes from  [crawdad](http://crawdad.cs.dartmouth.edu), 
but the `*.lucene.raw` files contain the processes trades in form of Lucene database.  You can access Lucene using many language. 
I use PHP.  Java is also common. 

The following structures can be found in Lucene databases.  All `data` is in JSON format but strigified and made safe via base64, i.e.  `base64( astext( json))`.
People who use these datatypes should know what they are.

```js
{ type: 'info', data: { ids:{id:count}, xs, ys, times}}  
{ type: 'frame', data: { xmin, xmax, ymin, ymax}}  
{ type: 'bygrid', data: { 'x,y': count, ...}}
{ type: 'byid', key(id), data: {count: { id, time, x, y, xraw, yraw}, ...}}
{ type: 'byxy', key(XxY), data: [ { id, time, x, y, xraw, yraw}, ...]}
{ type: 'bytime', key(%06d of time), data: [ { id, time, x, y, xraw, yraw}, ...]}
{ type: 'vizmap', key: 'density|speed|diff', data: { xtick, ytick, H: { 'x,y': eval,...}, raw:{ 'x,y': { key: count}}}}    diff>0#dense+still  diff<0:sparse+fast
```


# XYZ and WiFi scan traces

These are all the `*bz64jsonl` files starting with `xyzsw` prefix.  XYZSW stands for accelerometer *xyz* coordinates, *speed* calculated from XYZ, 
and results obtained from *WiFi* scans. All traces are captured on Android devices.  These are, in fact, in the processed form as raw traces are in textual form and 
are dumpted to separate files (XYZ and WiFi scan frequencies are different). 

The `*.bz64jsonl` files are in the simple format where each line is the `base64( bz2( astext( json)))` form. Note that, compared to the earlier format, the `bz2` compression 
is added.  Practice shows that it helps by compressing content by about 30-40 percent.  The `.bz64jsonl` files themselves also compress fairly well.  
Why such a messy format?  It is nice to have a given dataset in a single file.  Fast and easy to read and process further. 

Note that there are `*.example.json` files added to some of the `*.bz64jsonl` files.  Those show examples of the data stored in the `*.bz64jsonl` files by picking a single line 
and putting it in a separate `json` file.  Currently, the easiest way to view `json` files is to drop them into Firefox -- they come in colors, with folding, and everything. 


That is all for now. 


