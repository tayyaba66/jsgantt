# Using JSGantt #

### 1. Include JSGantt CSS and Javascript ###
```
<link rel="stylesheet" type="text/css" href="jsgantt.css" />
<script language="javascript" src="jsgantt.js"></script>
```

### 2. Create a div element to hold the gantt chart ###
```
<div style="position:relative" class="gantt" id="GanttChartDIV"></div>
```

### 3. Start a SCRIPT block ###
```
<script language="javascript">
```

### 4. Instantiate JSGantt using GanttChart() ###
```
var g = new JSGantt.GanttChart('g',document.getElementById('GanttChartDIV'), 'day');
```


GanttChart(pGanttVar, pDiv, pFormat)
pGanttVar: (required) name of the variable assigned
pDiv: (required) this is a DIV object created in HTML
pFormat: (required) - used to indicate whether chart should be drawn in "day", "week", or "month" format

Customize the look and feel using the following setters
```
g.setShowRes(1); // Show/Hide Responsible (0/1)
g.setShowDur(1); // Show/Hide Duration (0/1)
g.setShowComp(1); // Show/Hide % Complete(0/1)
g.setCaptionType('Resource');  // Set to Show Caption (None,Caption,Resource,Duration,Complete)
g.setShowStartDate(1); // Show/Hide Start Date(0/1)
g.setShowEndDate(1); // Show/Hide End Date(0/1)
g.setDateInputFormat('mm/dd/yyyy')  // Set format of input dates ('mm/dd/yyyy', 'dd/mm/yyyy', 'yyyy-mm-dd')
g.setDateDisplayFormat('mm/dd/yyyy') // Set format to display dates ('mm/dd/yyyy', 'dd/mm/yyyy', 'yyyy-mm-dd')
g.setFormatArr("day","week","month","quarter") // Set format options (up to 4 : "minute","hour","day","week","month","quarter")

```
### 5. Add Tasks using AddTaskItem() ###

```
g.AddTaskItem(new JSGantt.TaskItem(1,   'Define Chart API',     '',          '',          'ff0000', 'http://help.com', 0, 'Brian',     0, 1, 0, 1));
g.AddTaskItem(new JSGantt.TaskItem(11,  'Chart Object',         '2/10/2008', '2/10/2008', 'ff00ff', 'http://www.yahoo.com', 1, 'Shlomy',  100, 0, 1, 1));
```
TaskItem(pID, pName, pStart, pEnd, pColor, pLink, pMile, pRes, pComp, pGroup, pParent, pOpen, pDepend)

pID: (required) is a unique ID used to identify each row for parent functions and for setting dom id for hiding/showing

pName: (required) is the task Label

pStart: (required) the task start date, can enter empty date ('') for groups. You can also enter specific time (2/10/2008 12:00) for additional percision or half days.

pEnd: (required) the task end date, can enter empty date ('') for groups

pColor: (required) the html color for this task; e.g. '00ff00'

pLink: (optional) any http link navigated to when task bar is clicked.

pMile:(optional) represent a milestone

pRes: (optional) resource name

pComp: (required) completion percent

pGroup: (optional) indicates whether this is a group(parent) - 0=NOT Parent; 1=IS Parent

pParent: (required) identifies a parent pID, this causes this task to be a child of
identified task

pOpen: UNUSED - in future can be initially set to close folder when chart is first drawn.
You should be able to add items to the chart in realtime via javascript and issuing "g.Draw()" command.


### 5a. Another way to add tasks is to use an external XML file with parseXML() ###

```
JSGantt.parseXML("project.xml",g);
```
The structure of the XML file:
```
<project> <task> <pID>10</pID> <pName>WCF Changes</pName> <pStart></pStart> <pEnd></pEnd> <pColor>0000ff</pColor> <pLink></pLink> <pMile>0</pMile> <pRes></pRes> <pComp>0</pComp> <pGroup>1</pGroup> <pParent>0</pParent> <pOpen>1</pOpen> <pDepend /> </task> <task> <pID>20</pID> <pName>Move to WCF from remoting</pName> <pStart>8/11/2008</pStart> <pEnd>8/15/2008</pEnd> <pColor>0000ff</pColor> <pLink></pLink> <pMile>0</pMile> <pRes>Rich</pRes> <pComp>10</pComp> <pGroup>0</pGroup> <pParent>10</pParent> <pOpen>1</pOpen> <pDepend></pDepend> </task> <task> <pID>30</pID> <pName>add Auditing</pName> <pStart>8/19/2008</pStart> <pEnd>8/21/2008</pEnd> <pColor>0000ff</pColor> <pLink></pLink> <pMile>0</pMile> <pRes>Mal</pRes> <pComp>50</pComp> <pGroup>0</pGroup> <pParent>10</pParent> <pOpen>1</pOpen> <pDepend>20</pDepend> </task> </project>
```
### 6. Call Draw() and DrawDependencies() ###


```
g.Draw();	
g.DrawDependencies();
```


### 7. Close the 

&lt;script&gt;

 block ###
```
</script>
```

### Final code ###
The resulting code should look like:
```
<link rel="stylesheet" type="text/css" href="jsgantt.css" />
<script language="javascript" src="jsgantt.js"></script>
<div style="position:relative" class="gantt" id="GanttChartDIV"></div>
<script>

  var g = new JSGantt.GanttChart('g',document.getElementById('GanttChartDIV'), 'day');
  g.setShowRes(1); // Show/Hide Responsible (0/1)
g.setShowDur(1); // Show/Hide Duration (0/1)
g.setShowComp(1); // Show/Hide % Complete(0/1)

  if( g ) {

    g.AddTaskItem(new JSGantt.TaskItem(1,   'Define Chart API',     '',          '',          'ff0000', 'http://help.com', 0, 'Brian',     0, 1, 0, 1));
    g.AddTaskItem(new JSGantt.TaskItem(11,  'Chart Object',         '2/10/2008', '2/10/2008', 'ff00ff', 'http://www.yahoo.com', 1, 'Shlomy',  100, 0, 1, 1));
    g.AddTaskItem(new JSGantt.TaskItem(12,  'Task Objects',         '',          '',          '00ff00', '', 0, 'Shlomy',   40, 1, 1, 1));
    g.AddTaskItem(new JSGantt.TaskItem(121, 'Constructor Proc',     '2/21/2008', '3/9/2008',  '00ffff', 'http://www.yahoo.com', 0, 'Brian T.', 60, 0, 12, 1));
    g.AddTaskItem(new JSGantt.TaskItem(122, 'Task Variables',       '3/6/2008',  '3/11/2008', 'ff0000', 'http://help.com', 0, '',         60, 0, 12, 1,121));
    g.AddTaskItem(new JSGantt.TaskItem(123, 'Task Functions',       '3/9/2008',  '3/29/2008', 'ff0000', 'http://help.com', 0, 'Anyone',   60, 0, 12, 1));
    g.AddTaskItem(new JSGantt.TaskItem(2,   'Create HTML Shell',    '3/24/2008', '3/25/2008', 'ffff00', 'http://help.com', 0, 'Brian',    20, 0, 0, 1,122));
    g.AddTaskItem(new JSGantt.TaskItem(3,   'Code Javascript',      '',          '',          'ff0000', 'http://help.com', 0, 'Brian',     0, 1, 0, 1));
    g.AddTaskItem(new JSGantt.TaskItem(31,  'Define Variables',     '2/25/2008', '3/17/2008', 'ff00ff', 'http://help.com', 0, 'Brian',    30, 0, 3, 1));
    g.AddTaskItem(new JSGantt.TaskItem(32,  'Calculate Chart Size', '3/15/2008', '3/24/2008', '00ff00', 'http://help.com', 0, 'Shlomy',   40, 0, 3, 1));
    g.AddTaskItem(new JSGantt.TaskItem(33,  'Draw Taks Items',      '',          '',          '00ff00', 'http://help.com', 0, 'Someone',  40, 1, 3, 1));
    g.AddTaskItem(new JSGantt.TaskItem(332, 'Task Label Table',     '3/6/2008',  '3/11/2008', '0000ff', 'http://help.com', 0, 'Brian',    60, 0, 33, 1));
    g.AddTaskItem(new JSGantt.TaskItem(333, 'Task Scrolling Grid',  '3/9/2008',  '3/29/2008', '0000ff', 'http://help.com', 0, 'Brian',    60, 0, 33, 1));
    g.AddTaskItem(new JSGantt.TaskItem(34,  'Draw Task Bars',       '',          '',          '990000', 'http://help.com', 0, 'Anybody',  60, 1, 3, 1));
    g.AddTaskItem(new JSGantt.TaskItem(341, 'Loop each Task',       '3/26/2008', '4/11/2008', 'ff0000', 'http://help.com', 0, 'Brian',    60, 0, 34, 1));
    g.AddTaskItem(new JSGantt.TaskItem(342, 'Calculate Start/Stop', '4/12/2008', '5/18/2008', 'ff6666', 'http://help.com', 0, 'Brian',    60, 0, 34, 1));
    g.AddTaskItem(new JSGantt.TaskItem(343, 'Draw Task Div',        '5/13/2008', '5/17/2008', 'ff0000', 'http://help.com', 0, 'Brian',    60, 0, 34, 1));
    g.AddTaskItem(new JSGantt.TaskItem(344, 'Draw Completion Div',  '5/17/2008', '6/04/2008', 'ff0000', 'http://help.com', 0, 'Brian',    60, 0, 34, 1));



    g.Draw();	
    g.DrawDependencies();


  }
  else
  {
    alert("not defined");
  }

</script>
  
```