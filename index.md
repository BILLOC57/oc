<html lang="en">
<head>
  <meta charset="utf-8">
  <title>California Covid19 Estimator</title>
  <link rel="stylesheet" href="//code.jquery.com/ui/1.12.1/themes/eggplant/jquery-ui.css">
  <script src="//code.jquery.com/jquery-1.12.4.js"></script>
  <script src="//code.jquery.com/ui/1.12.1/jquery-ui.js"></script>
</head>
<body>

<h4 style="font-family: sans-serif">Select a day to display the projected <br>number of Corona virus cases in <br>California</h4>

<p style="font-family: sans-serif">See <a id="dexplain" href="#">Detailed explaination</a></p>

<div class="ui-widget-overlay ui-front" id="popup">
</div>
  <div id="txt"  style="position: absolute; width: 320px; left: 50px; top: 30px; padding: 1.2em; overflow-x: hidden;" class="ui-widget ui-front ui-widget-content ui-corner-all ui-widget-shadow">
    <button id="hider">Close</button>
    <p>
	I decided to put some of these Corona Virus statistics for California in a spreadsheet and take a look at them. My source was <a href="https://en.wikipedia.org/wiki/2020_coronavirus_pandemic_in_California">This</a> It seemed as if there were anomalies in some of the early and later numbers so I arbitrarily based the overnight growth rate on the average rates for the week between Mar 7th and Mar 13th. Using that growth rate and starting w/ the number of cases on Mar 7 (88) provides daily exponentially growing case numbers that were consistently below what was actually reported (between the 7th & 27th). (1) Therefore if anything my calculations are an underestimate. 
   </p>
    <p>
	What I found is that, at the rate we’re going, by Apr 6th, the supposed end of the “Bay Area Shelter In Place” restrictions there will be some twenty – three – thousand cases in the state. <br>By the end of April there will be more than two – million (almost ten times today’s, Mar 19th, worldwide count). That’s how exponential growth works. That’s how important ‘flattening the curve’ is. 
    </p>
    <p>
	Also you’ll be to tell whether or not the restrictions did the trick. If you look at the number of cases on Apr 6th then either they will be around twenty – three – thousand, above, or below it. The restrictions will Only have worked in the Last Case. 
    </p>
    <p>
	(1) - Keep in mind that ANY statistics around all this are muddled by the fact that initially American ability to test for the Corona Virus was essentially nonexistent, and was subsequently extremely limited and awkward. It wouldn’t be difficult to improve upon that, so we can attribute a debatable amount of the increase in case numbers to expanded access to testing. 
    </p>
  </div>
<div id="datepicker"></div>
<br>
<p style="font-family: sans-serif">Click a Date to see a Result</p> 
<script>
var	minInHr = secInMin = 60, msInSec = 1000, hrInDay = 24;
var	msInDay = minInHr * secInMin * msInSec * hrInDay;
var	minDate = new Date("March 8, 2020"), maxDate = new Date("May 30, 2020");

var	startDate = new Date("March 7, 2020");
var	startCount = 88;
var	growthRate = 0.204285714; // 20.43%

function diff(tgtDate){ return Math.ceil( (tgtDate - startDate) / msInDay ); }
function eexp(days){  
  return startCount * Math.pow(1+growthRate, days);
}
function fmt(num){ return "Number of cases: " + Number(num).toFixed(2).replace(/(\d)(?=(\d{3})+(?!\d))/g, '$1,'); }

$( "#datepicker" ).datepicker({
	minDate: minDate,
	maxDate: maxDate
});
function tgl() { $( "#popup" ).toggle(); $( "#txt" ).toggle(); }

$( "#datepicker" ).change( function(){ 
  $( "#result" ).text(
    fmt(
      eexp(
        diff(
          $( "#datepicker" ).datepicker("getDate")  
        )
      )
    )
  ); 
} );
$( "#hider, #dexplain" ).click( 
function() { tgl(); }
);

tgl();

</script>
 
</body>
</html>
