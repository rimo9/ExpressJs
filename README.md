# ExpressJs ToDo App

## Vaja installida:
Nodejs https://nodejs.org/en/download/

# Rakenduse tegemine

## Installi express, application generator tool ja nodemon
```
npm install express -g
npm install express-generator -g
npm install nodemon -g
```

## Loo express app nimega todo, mis kasutab pug view enginit
```
express --view=pug todo
```

## Mine todo kausta, installi dependancies
```
npm install
```

## Rakenduse käivitamine
```
npm start
```

## Rakenduse käivitamine nodemoniga
```
nodemon bin/www
```

# Todo tegemine

## views/index.pug failis peale "block contenti" pane veebis kuvatav kood
```
h1 ToDo App
h2 Add New Task
div
	form(
		action="/addtask"
		method="POST")
		input(
			type="text"
			name="newtask"
			placeholder="add new task")
		button Add Task
h2 ToDo
div
	each item in task
		form(
			action="/removetask"
			method="Post")
			li= item
				input(
					type="hidden"
					name="removetask"
					value=item)
				button Remove
h2 Finished
div
	each item in complete
		li= item
```

## routes/index.js failis loo kaks uuta variablet
```
var task = [];
var complete = [];
```

## GET home page funktsiooni sees asenda res.render
```
res.render('index', { title: 'Express', task: task, complete: complete });
```

## Peale GET home page funktsiooni lisa funktsioonid uute taskide lisamiseks ja vanade eemaldamiseks
```
/* POST newtask */
router.post("/addtask", function(req, res) {
    var newTask = req.body.newtask;
    task.push(newTask);
    res.redirect("/");
});

/* POST removetask */
router.post("/removetask", function(req, res) {
    var completeTask = req.body.removetask;
	task.splice(task.indexOf(completeTask), 1);
	complete.push(completeTask);
    res.redirect("/");
});
```

## CSS public/stylesheets/style.css
```
body {
  font: 14px "Lucida Grande", Helvetica, Arial, sans-serif;
  text-align:center;
  position: absolute;
  margin: auto;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  width: 300px;
  height: 700px;
  border-radius: 3px;
}

a {
  color: #00B7FF;
}

h1 {
	text-align:center;
}

h2 {
	text-align:center;
	border-bottom:1px solid #b1c9bb;
}

li {
	text-align:center;
	list-style-type: none;
	margin-bottom:2px;
	border-bottom:1px dotted #CCC;
	max-width: 300px;
	padding:10px;
	margin-bottom:10px;
}

div {
	padding:10px 15px;
	border:2px solid #b1c9bb;
	border-radius:5px;
	background:#FFF;
	margin:15px 0;
}

button {
	margin-left: 10px;
	float:right;
}
```