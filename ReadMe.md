# Fun/Pain with Python Packaging

It all started a Saturday morning, when I came cross [this LinkedIn post](https://www.linkedin.com/posts/maria-vechtomova_why-not-tell-people-to-simply-use-pyenv-activity-7182014679395766272-Rl9D) over coffee ☕ 

The post is about the always interesting and spicy topic of `python packaging pain` 🤪 

The article recommended in the post is hilarious 🤣 and definately worth a read. I am saving it here so I can read it again. (link: [Why not tell people to "simply" use pyenv, poetry or anaconda](https://www.bitecode.dev/p/why-not-tell-people-to-simply-use))

Anyway, back to the tool recommended in the article, which is `venv`. 😎 I only used `vevn` very briefly at the beginning of my python journey, then moved on to tools like `pipenv` and `anaconda` which the article critisized about. In the name of fun and exploration, let me do `venv` again and document my learning on the way. I will follow the instruction from the [official `venv` doc](https://docs.python.org/3/library/venv.html) and do my best not to "stackoverflow my way out of suffering" (To be honest, I can't remember how many times stackoverflow saved my life ❤️)

I will try to accomplish three things. 

1. Create the `.venv` using a particular python version ✅
2. Active and use the `.venv` ✅
3. Share the `.venv` so it is reproducible

Wish me luck! 🤞

# Steps

## 1. Create the `.venv`

### 1.1 Check for available python versions

* I have multiple python versions available in anaconda, but lets don't use it for this experiment.
* Check the default Global python version: `python --version`.    
    * find path to it:
    * run `python -c "import os, sys; print(os.path.dirname(sys.executable))"`, or 
    * run `python -m identify_python_path` while in this repo's root folder 
* How do I find out about other Pythons versions available in my machine? 
    * typically for windows it is saved in `C:\Users\<username>\AppData\Local\Programs\Python\Python3X`
    * or run `py --list-paths`

### 1.2 Create a venv using a particular python version

* Check whether the desired python version is available. 
* If not, install using the official installer at `python.org`, for example [windows installer available here](https://www.python.org/downloads/windows/)
* After installation, run the command below (for windows)
`C:\Users\<username>\AppData\Local\Programs\Python\Python3X\python -m venv PATH-to-REPO\.venv` 
    * one could also use `py -3.x -m venv` to specify python version but I opted to specify where exactly this python sits, since `py --lists-paths` give me interesting results due to my installation history. 🙈  
* This is where I used to stumble before. 
    * If I don't specify the path to the particular python version, it would always just used the default. 
    * If I revise the environment path variable to prioritize this desired python version, it would then become the new default. 
    * In contrast, the solution above gives us the flexibility to create a `.venv` with whichever python version we see fit for each particular project. 

## 2. Activate and use the `.venv`
* Following the instruction from [official `venv` doc](https://docs.python.org/3/library/venv.html), you can activate the environment using `.venv/Scripts/activate` (windows)
    * In windows you could have this error: `.venv/Scripts/activate : File path-to-project\.venv\Scripts\Activate.ps1 cannot be loaded because running scripts is disabled on this system. `
    * In this case, run `Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser`
* `python -m pip install` any pakcages needed (Why not `pip install` directly? 🧐 [here is a discussion](https://www.bitecode.dev/p/relieving-your-python-packaging-pain))

## 3. Share the `.venv`
* To export the environment
    * `Freeze` the environemnt for the project using `python -m pip freeze > requirements_py310.txt`
    * One of the important reasons that I switched from `venv` to `pipenv` was because python version was natually specified in `pipenv`'s lockfile `Pipfile.lock`. But this is not the case with `requimrenets.txt`. 
    * Fortunately as shown above, it is pretty straightforward to utilize specific python versions for `venv` implementations too, one just need to be mindful and specify it while creating the environment. 
    * Therefore, I personaly prefer to specify python version at the title of the requirements like `requirements_py3xx`, which can serve as a reminder to myself and everyone who wants to replicate the environment re: which python version is needed for this `venv`.
* To replicate the environment
    * Create the `venv` with the specific version (see step 1 above)
        * if exist already, run `Remove-Item -Path ".venv" -Recurse -Force` in powershell 
    * Activate the `venv` (see step 2 above)
    * then `python -m pip install -r requirements_py310.txt` 


