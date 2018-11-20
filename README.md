# ExpressJs ToDo App

## Vaja installida:
Nodejs https://nodejs.org/en/download/

# Rakenduse tegemine

## Installi express ja application generator tool
```
npm install express -g
npm install express-generator -g
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

# Todo tegemine

## views/index.pug failis peale "block contenti" pane veebis kuvatav kood
```
h1 ToDo App
h2 Add New Task
form(
	action="/addtask"
	method="POST")
	input(
		type="text"
		name="newtask"
		placeholder="add new task")
	button Add Task
h2 ToDo
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