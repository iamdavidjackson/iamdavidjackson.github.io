---
layout: post
title: "Myth Buster - HTTP Request Count Performance Tests"
description: 
headline: 
modified: 2015-08-03
category: webdevelopment
tags: [myth busters, http, javascript]
imagefeature: 
mathjax: 
chart: 
comments: true
featured: true
---

Ok lets test the age old theory that having multiple HTTP requests to get Javascript is adverse to loading times.  Obviously it is better to download a single file over multiple files however what I'm wondering is, how much better?  Are we killing ourselves trying to reduce HTTP requests when there is no benefit or are we saving the world from certain destruction?  Lets have a go shall we?


## 1 vs 2 JS files
Load 1 concatenated JS file or 2 single ones

<button onClick="runTestTwo();">Run Test</button>

## 1 vs 5 JS files
Load 1 concatenated JS file or 5 single ones

<button onClick="runTestFive();">Run Test</button>

## 1 vs 10 JS files
Load 1 concatenated JS file or 10 single ones

<button onClick="runTestTen();">Run Test</button>


<script src="https://cdnjs.cloudflare.com/ajax/libs/require.js/2.1.20/require.min.js"></script>
<script>
	requirejs.config({
	    baseUrl: '/assets/js/posts/http/',
	    paths: {
	        test: 'test'
	    },
	    bundles: {
	    	'concattwo': ['testone', 'testtwo'],
	    	'concatfive': ['testthree', 'testfour', 'testfive', 'testsix', 'testseven'],
	    	'concatten': ['testeight', 'testnine', 'testten', 'testeleven', 'testtwelve', 'testthirteen', 'testfourteen', 'testfifteen', 'testsixteen', 'testseventeen']
	    }
	});

	function runTestTwo() {
		var startTime;

		startTime = Date.now();
		var test = require(['onetest', 'twotest'], function(test) {
			var endTime = Date.now();
			var duration = endTime - startTime;
			console.log('getting 2 files took ' + duration + 'ms.');
		});

		startTime = Date.now();
		var testTwo = require(['testone', 'testtwo'], function(test) {
			var endTime = Date.now();
			var duration = endTime - startTime;
			console.log('getting 1 file took ' + duration + 'ms.');
		});
	}

	function runTestFive() {
		var startTime;

		startTime = Date.now();
		var test = require(['threetest', 'fourtest', 'fivetest', 'sixtest', 'seventest'], function(test) {
			var endTime = Date.now();
			var duration = endTime - startTime;
			console.log('getting 5 files took ' + duration + 'ms.');
		});

		startTime = Date.now();
		var testTwo = require(['testthree', 'testfour', 'testfive', 'testsix', 'testseven'], function(test) {
			var endTime = Date.now();
			var duration = endTime - startTime;
			console.log('getting 1 file took ' + duration + 'ms.');
		});
	}

	function runTestTen() {
		var startTime;

		startTime = Date.now();
		var test = require(['eighttest', 'ninetest', 'tentest', 'eleventest', 'twelvetest', 'thirteentest', 'fourteentest', 'fifteentest', 'sixteentest', 'seventeentest'], function(test) {
			var endTime = Date.now();
			var duration = endTime - startTime;
			console.log('getting 10 files took ' + duration + 'ms.');
		});

		startTime = Date.now();
		var testTwo = require(['testeight', 'testnine', 'testten', 'testeleven', 'testtwelve', 'testthirteen', 'testfourteen', 'testfifteen', 'testsixteen', 'testseventeen'], function(test) {
			var endTime = Date.now();
			var duration = endTime - startTime;
			console.log('getting 1 file took ' + duration + 'ms.');
		});
	}


</script>