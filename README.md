<div align="center">

## Javascript Calendar


</div>

### Description

Want a calendar on a HTML-page ???

This is just a SIMPLE!!! calender application written in Javascript. It's to you out there to alter it. It's usable for automatically filling date fields on html forms.

Tested for internet explorer 6 or netscape 6.2,

but I think it also works on IE5, IE5.5, NS6, NS6.1
 
### More Info
 


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Bert De Verschrikkelijke](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/bert-de-verschrikkelijke.md)
**Level**          |Advanced
**User Rating**    |4.1 (29 globes from 7 users)
**Compatibility**  |
**Category**       |[Internet/ Browsers/ HTML](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/internet-browsers-html__2-68.md)
**World**          |[Java](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/java.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/bert-de-verschrikkelijke-javascript-calendar__2-2771/archive/master.zip)





### Source Code

```
<HTML>
<HEAD>
<style type=text/css>
body { font-family: arial, helvetica, helv }
.rightday{ color: green; cursor: pointer; cursor:hand; }
.rightmonth { color: red;cursor: pointer; cursor:hand; }
.wrongmonth { color: blue; cursor: pointer; cursor:hand; }
div { font-weight: bold; cursor: pointer; cursor: hand; }
</style>
</HEAD>
<BODY>
<SCRIPT LANGUAGE=JAVASCRIPT>
/*
this code written by Bert De Verschrikkelijke march 23 - 2002
this code was written to be used, so alter it all you want
Tested for internet explorer 6 or netscape 6.2,
but I think it also works on IE5, IE5.5, NS6, NS6.1
Special thanks to Vojimir Bato Kecman and Vitan Minchev for bug reporting.
*/
var minYear = 1995;
var maxYear = 2010;
var minMonth = 0;
var maxMonth = 11;
function formatDate(argDate) {
  var tmpYear = String(argDate.getFullYear());
  var tmpMonth = String(argDate.getMonth()+1);
  var tmpDate = String(argDate.getDate());
  tmpDate = ((tmpDate.length==1)? '0':'') + String(tmpDate);
  tmpMonth = ((tmpMonth.length==1)? '0':'') + String(tmpMonth);
  return(tmpDate + tmpMonth + tmpYear);
}
function getDayLabel(argNum) {
  switch(argNum) {
    case 0: return('Zo'); case 1: return('Ma'); case 2: return('Di');
    case 3: return('Wo'); case 4: return('Do'); case 5: return('Vr');
    case 6: return('Za');
  }
}
function getMonthLabel(argNum) {
  switch(argNum) {
    case 0: return('Januari');case 1: return('Februari'); case 2: return('Maart');
    case 3: return('April'); case 4: return('Mei');case 5: return('Juni');
    case 6: return('Juli');case 7: return('Augustus'); case 8: return('September');
    case 9: return('October');case 10: return('November'); case 11: return('December');
  }
}
today = new Date();
useMonth = today.getMonth();
useYear = today.getFullYear();
hT = '';
hT+= '<TABLE><TR><TD><SELECT id="selMonth" onchange="useMonth=this.value;writeDate();">';
for (var i=minMonth; i<=maxMonth; i++)
hT+= '<OPTION value="' + i + '" ' + ((i==useMonth)?'SELECTED':'') + '>' + getMonthLabel(i) + '</OPTION>';
hT+= '</SELECT></TD>';
hT+= '<TD align=right><SELECT id="selYear" onchange="useYear=this.value;writeDate();">';
for (var i=minYear; i<=maxYear; i++)
hT+= '<OPTION value="' + i + '" ' + ((i==useYear)?'SELECTED':'') + '>' + i + '</OPTION>';
hT+= '</SELECT></TD></TR>';
hT+= '<TR><TD colspan=2><DIV id="calendar" style="width: "></DIV></TD></TR>';
hT+= '<TR><TD colspan=2>';
hT+= '<TABLE cellpadding=0 cellspacing=0 border=0 width=100%>';
hT+= '<TR>';
hT+= '<TD align=center width=15%><DIV onclick="showPrevYear()"><<</DIV></TD>';
hT+= '<TD align=center width=15%><DIV onclick="showPrevMonth()"><</DIV></TD>';
hT+= '<TD align=center><DIV onclick="showToday()">vandaag</DIV></TD>';
hT+= '<TD align=center width=15%><DIV onclick="showNextMonth()">></DIV></TD>';
hT+= '<TD align=center width=15%><DIV onclick="showNextYear()">>></DIV></TD>';
hT+= '</TR>';
hT+= '</TABLE>';
hT+= '</TD></TR>';
hT+= '</TABLE>';
document.write(hT);
function setSelected(argSelBoxRef, argValue) {
  for (var z=0; z < argSelBoxRef.options.length; z++)
  argSelBoxRef.options[z].selected = (argSelBoxRef.options[z].value == argValue);
}
  function showPrevYear() {
  var yearSel = document.getElementById('selYear');
  useMonth = document.getElementById('selMonth').value;
  useYear = yearSel.value;
  useYear--;
  if (useYear < minYear) useYear = maxYear;
  setSelected(yearSel, useYear);
  writeDate();
}
function showNextYear() {
  var yearSel = document.getElementById('selYear');
  useMonth = document.getElementById('selMonth').value;
  useYear = yearSel.value;
  useYear++;
  if (useYear > maxYear) useYear = minYear;
  setSelected(yearSel, useYear);
  writeDate();
}
function showPrevMonth() {
  var monthSel = document.getElementById('selMonth');
  useYear = document.getElementById('selYear').value;
  useMonth = monthSel.value;
  useMonth--;
  if (useMonth < minMonth) {
    showPrevYear();
    useMonth = maxMonth;
  }
  setSelected(monthSel, useMonth);
  writeDate();
}
function showNextMonth() {
  var monthSel = document.getElementById('selMonth');
  useYear = document.getElementById('selYear').value;
  useMonth = monthSel.value;
  useMonth++;
  if (useMonth > maxMonth) {
    showNextYear();
    useMonth = minMonth;
  }
  setSelected(monthSel, useMonth);
  writeDate();
}
function showToday() {
  var monthSel = document.getElementById('selMonth');
  var yearSel = document.getElementById('selYear');
  useMonth = today.getMonth();
  useYear = today.getFullYear();
  setSelected(monthSel, useMonth);
  setSelected(yearSel, useYear);
  writeDate();
}
function writeDate() {
  var tdextra='';
  var stylecls='';
  var oneDay = 86400000;
  var twelveHours = 43200000;
  var countDate = new Date( useYear, useMonth, 1);
  countDate = new Date( countDate.valueOf() - ( countDate.getDay() * oneDay) + twelveHours);
  hT = '';
  hT+= '<TABLE border=1>';
  for (var r=0; r<7; r++) {
    hT += '<TR>';
    for (var c=0; c<7; c++) {
      if (r==0) {
        tdextra = 'align=center';
        cell = getDayLabel(c);
      }
      else {
        if (countDate.getMonth() == useMonth )
          stylecls = ( ( (countDate.getDate() == today.getDate() ) &&
                  (countDate.getFullYear() == today.getFullYear() ) &&
                  (countDate.getMonth()== today.getMonth() ) )? 'rightday' : 'rightmonth' );
        else
          stylecls = 'wrongmonth';
        cell = ' ' + countDate.getDate() + ' ';
        tdextra = 'class="' + stylecls + '" onclick="alert(\'' + formatDate(countDate) + '\');" align=right';
      }
      hT += '<TD ' + tdextra + '>' + cell + '</TD>';
      if (r!=0) countDate = new Date(countDate.valueOf() + oneDay );
    }
    hT += '</TR>';
  }
  hT+= '</TABLE>';
  document.getElementById('calendar').innerHTML = hT;
}
writeDate();
</SCRIPT>
</BODY>
</HTML>
```

