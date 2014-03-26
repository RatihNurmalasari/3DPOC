Auto Derivation of Test Context
===============================


Description
-----------

Easy-tag-automation is created to enable ease the process of functional automation. The idea is to embed a test-driven tag directly in the HTML itself for the engine to derive the the context of a particular test. On top of a well known automation's goal, our additional goals to create the framework are as follow:

* Enable non-engineers with familiarity of HTML and basic Javascript to automate functional testing with minimal coding. This would allow people who typically only do manual testing to be involved in automation process
* Introduce the context of test cases as early as the design phase instead of an after thought. By embedding as part of the HTML, the design, engineers and QA team can collaborate together on the test cases prior to actual development following the spirit of TDD
* Derivation of test cases by inspecting the code combined with test metadata to eliminate Selector driven test cases and replaced by semantic tag driven test context 
* Minimize the need to rewrite the test cases (or in this case the metadata) as the UI undergoing changes

Quickstart
----------

At the very basic, after setting the test context within the HTML tag, the following metadata is what we need in order to execute the test:

<pre>
TEST.runtime = {
	"testName": "Product List",
	"test-cases": [
		{
			"description" : "Enter keyword and perform search",
			"event": "search",
			"input" : ["Yellow Gold"],
			"action" : "click",
			"assert-for": ["Search Result 1"]
		}
	]
};
</pre>

The above metadata is basically saying the following:
* Find me the event related to "search" 
* For this event, I want to input "Yellow Gold"
* I want a click on the "search" event
* Finally I will do my assertions by checking if "Search Result 1" matches with the text in the search result

The metadata itself (for event, input and assertions) is mapped to the test tag embedded in the HTML. These tags are as follow:
+ Define an actionable event on the page by identifying the tag in the HTML. This could be a button that the user will press or a key press on search box. You marked them with <i>test-event</i> with a unique identifier. An example below show that we want to create actionable event on the img tag 
<pre>
&lt; img src="../../assets/images/icons/search-ico.png" alt="Search" test-event="search" /&gt;
</pre>
+ To mark the input for a particular actionable event, you marked them with <i>test-input</i> tag tied with the event name. You can have more than one input for a particular tag (such as the event related to registering a new user). Additionally, an input can be used for more than on event. Following the example above, you would mark the input box for search as follow 
<pre>
&lt;input type="text" value="Search" test-input="search" /&gt;
</pre>
+ Finally you mark the assertion by embedding <i>test-assert</i> tag in the element where the assertions will be performed. You can have as many assertions as you need. In the case above, you will tag the search result as follow 

<pre>
&lt;div class="search-result"&gt;
	&lt;ul&gt;
		&lt;li test-assert="search">Search result 1&lt;/li&gt;
		&lt;li test-assert="search" >Search result 2&lt;/li&gt;
		&lt;li test-assert="search">Search result 3&lt;/li&gt;
		&lt;li test-assert="search">Search result 4&lt;/li&gt;
	&lt;/ul&gt;
&lt;/div&gt;
</pre>

The event, input and assertions are all group under the same event which allow the framework to derive the context of a particular text without tight coupling the test with the UI. As the UI changes, as long as the test tags are put in appropriate place, there is no need to rewrite the test to adjust to a new selectors

You could see the sample of a test case in action by going to photon-test-automation-poc/content/home/01_HP_B.html within the source code
