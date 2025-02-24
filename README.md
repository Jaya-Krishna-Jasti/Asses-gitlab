# 1. Write a Ruby or Bash script that will print usernames of all users on a Linux system together with their home directories. 
Here&#39;s some example output:

		gitlab:/home/gitlab
		nobody:/nonexistent
		.
		.
Each line is a concatenation of a username, the colon character (:), and the home directory path for that username. Your script should output such a line for each user on the system.

Ans:

I am going to write a Ruby script that prints all the user names and their home directories within the Linux system.

Now where do we have all the user names and their home directories in Linux? They will be stored in the file path /etc/passwd here are the contents of the file.
Now we use cat command to view the contents of the file path /etc/passwd.

![Screenshot 2024-03-08 204132](https://github.com/jastijayakrishna/Assessment/assets/20278464/c0010632-fd55-406f-bc24-ffe44fee51a3)


 

The /etc/passwd is a plain text file in the Unix operating system that has information about user's accounts. Each line in the file represents a user and has several fields separated by a colon ‘:’. The fields are: 

![Screenshot 2024-03-13 151517](https://github.com/jastijayakrishna/Assessment/assets/20278464/701a2790-21b7-4df1-ba81-537b62ccbce1)

---

In the above image, we can see

**Index 0**: This is the username of the account.

**Index 1**: This is the password of the account which is represented by x or *. The actual password lies in /etc/shadow for obvious security reasons.

**Index 2**: A unique user ID is assigned to each user.

**Index 3**: This is the group ID number which corresponds to a group in ‘/etc/group’ file.

**Index 4**: This is used for user information or any other information.

**Index 5**: This represents the absolute path to the home directory.

**Index 6**: This is the absolute path to the user's default  shell program. 

---

Now we can see the username is present in the 0th index and the home directory is present in the 5th index. We are going to write a ruby script to open the file and loop all the contents in a variable named file

				File.open('etc/passwd/').each do |line| 

Now we are going to split the array of lines using colon ‘:’ as a delimiter because in the above picture, each word is separated by a colon.

				word = line.split(':')
 
Now we are going to take the required index from the line and assign it to the variable

				username = word[0]
				home_directory = word[5]

We are going to print the username and home_directory by puts command

				puts “#{username}: #{home_directory}”

Now the whole code looks like

				File.open('/etc/passwd').each do |line|
					word = line.split(':')
					username = word[0]
					home_directory = word[5]
					puts "#{username}: #{home_directory}"
				end
![Screenshot 2024-03-08 210416](https://github.com/jastijayakrishna/Assessment/assets/20278464/ac45616a-aa80-47f2-ba35-8125068fe986)

## Output:

![Screenshot 2024-03-08 210540](https://github.com/jastijayakrishna/Assessment/assets/20278464/d07599f4-3848-492e-a7c9-371cc7087d42)


## Sources: 

https://phoenixnap.com/kb/etc-passwd#:~:text=The%2Fetc%2Fpasswd%20file%20is,home%20directory%2C%20and%20default%20shell

Tools: ubuntu for testing and getting the output.

# 2. Study the Git commit graph shown below. What sequence of Git commands could have resulted in this commit graph?

   ![Screenshot 2024-03-14 200926](https://github.com/jastijayakrishna/Assessment/assets/20278464/9e752ba0-455c-4f29-800c-942ddb0ca99f)

Ans:

Now to get the desired commit graph we have to follow these git commands.


We have to initialize the git repository by using the init command in git.

				git init
					 
Now we make some changes to a file and now we prepare the file for staging and the dot(‘.’) represents the current directory. Here staging means preparing and organizing the changes essentially telling the git which 

modifications to include in the next commit.

				git add .
					 
Now we are going to commit the changes into git. Commit means git takes changes that are in the staging area and create a new “snapshot” of your repository at that point in time. This snapshot is added to the repository history. 

The  “ -m “ represents the message which is “First commit”.
                                        
				git commit -m “First commit”

The commit-graph after the first commit looks like this

![Screenshot 2024-03-08 123833](https://github.com/jastijayakrishna/Assessment/assets/20278464/13ae3ec9-4468-40f5-a626-e272eb2347a7)

      
Now we are going to make some more changes in a file and we will be staging it for the second commit
                                         
				git add.
      
Now we are going to do the second commit.
                                        
				git commit -m “Second commit”

The commit graph after the Second commit looks like this

![Screenshot 2024-03-08 123843](https://github.com/jastijayakrishna/Assessment/assets/20278464/516d7a20-50e6-49e6-81bd-844732db930b)


Now  we are going to create a branch named feature branch. A branch is a separate line of development within a repository that allows you to work independently without affecting the main line. We generally use a branch 

to develop features, fix bugs, or experiment with new ideas.

				git branch feature-branch
					
Now we created the branch to move into a new branch using the checkout command. It checks you into the new branch.

				git checkout feature-branch
					
We are now going to make some changes to the file and stage it.
                                       
				git add .
     
Now we are going to commit it with the message “Awesome feature”

                                        
				git commit -m “awesome feature”

The commit-graph after committing the awesome-feature looks like this


![Screenshot 2024-03-08 123855](https://github.com/jastijayakrishna/Assessment/assets/20278464/2b33e6af-1db6-4cc5-a26c-9c364e9debde)

     
Now we are going to move back to the master or main branch by using the command checkout.
                                        
				git checkout master
     
Now we are going to make some more changes in the file and stage it.
                                   
				git add .
     
Now we are going to commit it with the message “Third commit”.
                                        
				git commit -m “Third commit”

The commit-graph after the Third commit looks like this


![Screenshot 2024-03-08 123906](https://github.com/jastijayakrishna/Assessment/assets/20278464/5e0605a6-7c35-4538-b78d-0164d9430150)

     
We are going to merge the feature branch with  the master branch. 
                                        
				git merge feature-branch

This merge happened by using 'ort' strategy. ort stands for Ostensibly Recursive twin which is similar to the recursive strategy ( it works recursively finding a common ancestor i.e., basecommit between the branches and then applying the changes from each branch on top of that base. The difference between ort and recursive is mainly memory usage and performance.
     
Now we are going to make some more changes in the file and stage it.

				git add .
					 
Now we are going to commit it with the message “Fourth commit”.

				git commit -m “Fourth commit”



## The resulting commit graph looks like this

![Screenshot 2024-03-08 123816](https://github.com/jastijayakrishna/Assessment/assets/20278464/a9dac041-1253-45a0-bc0a-08108a305da5)

**Sources:**

I used AI tools to learn about ort strategy and gitkraken to get the final commit-graph.


# 3. Write a brief blog post for GitLab that explains what Git is and what it can do for you?

As a developer, I've learned to value Git's amazing power and versatility for code management. Git is a popular version control system that has transformed how developers work together and manage projects. In this blog 
post, I'll discuss my experiences with Git and how it has evolved into a vital tool in any development process.

Let's go back in time, Before git developers used to save their projects in different versions like project-v1, and project-v2. This is a cumbersome process because, in a professional setting, we can't track or share 
code changes while working in a team and everything has been done manually. Later we got a centralized version control system (CVS) and SVN provided a basic structure to this but had some limitations in branching and 
merging, requiring constant access to the server.

## What is git?

Git is a distributed version control system that is used to track the changes in a code while developing software. Linus Torvalds created it to support the Linux kernel. It allows the developers to work on the same 
project simultaneously, enabling them to track the changes, merge the code, and resolve the conflicts very effectively.

### What Git can do?

Here are some key features of Git

1. **Branching and Merging**: Basically, it is like a tree branch, which has a root node and different branches. In git branches allow developers to create separate lines of development which is useful for developing new 
features, Fixing bugs, or experimenting without affecting the main code.

To create a new branch and switch (‘-b’) to it we use:
                                   
				git checkout -b feature-branch

Merging is a process of integrating changes from one branch to another. It is most commonly used for combining branch changes into a main or master branch.

To merge a branch into the current branch we use:
		
				git merge feature-branch

2. **Staging Area**: This is the area where we prepare changes for a commit. We can selectively add the changes to our next commit, providing flexibility in how we organize our work.

To stage the changes we use
  	        
				git add filename

Committing Changes: Commit represents a snapshot of your project state at a particular point in time. They are the fundamental blocks of Git.

To commit staged changes with a message we use
		
				git commit -m “Add new feature”

3. **Remote Repositories**: With Git we can collaborate through remote repositories, which are hosted on Github, Gitlab, and Bitbucket. We can push our local changes to remote repositories and also pull changes made by others

To push our local commits to the remote repository we use:

				git push origin main

To pull changes from the remote repository we use:
 
				git pull origin main

History and Logs: Git provides us with a detailed history of our project allowing us to view all the past changes who made them and when they were made.

To view the commit history we use: 
 	
				git log

4. **Stashing**: It is a convenient way to temporarily save our work-in-progress changes without committing them. This will be useful particularly when we need to switch branches or contexts quickly, but you are not ready to 
commit your current changes. Modifications in our working directory and staging area are saved in the stash which allows us to revert to a clean working state.

To stash the changes we use:
 
				git stash

In conclusion, we can see how powerful git is  by offering features like version control, promoting teamwork, and code organization and what it can do to software development. By mastering these features we can enhance our workflow and keep our code base well structured.






**Sources:**

https://git-scm.com/book/en/v2






# 4. Tell me about a recent issue you debugged or a problem you solved. How did you go about debugging it? What tools did you use? What was the outcome?

Ans:

A student while I was web mentoring came to me with an issue stating that his mid-term web project was experiencing slow load times for a particular page where he displayed a list of items. It was taking too long to load 
which will impact the user experience.

## My Assessment:

First, we inspected the web page by going to the network tab and everything was fine there. Later, we moved to hitting the particular API using Postman but everything was working fine. Finally, I checked the logs of the application and server logs but couldn’t find any errors related to the loading page slowing down. It relatively seemed more like a performance issue rather than an error in the code or server. 

So we started analyzing the few SQL queries he wrote using the **EXPLAIN ANALYZE** command to see the performance of queries while fetching data.

## The Issue:

As we suspected, the slow load times were due to a database query that fetches the list of items. It’s taking a significant amount of time to load the page because of this issue. He is developing a retail site for the 
mid-term project and the query he’s using to fetch the data looks like this

				SELECT items.*, categories.name AS category_name, suppliers.name AS supplier_name
				FROM items
				JOIN categories ON items.category_id = categories.id
				JOIN suppliers ON items.supplier_id = suppliers.id
				WHERE items.price > 100
				ORDER BY items.name;

In this, he’s fetching all the columns from the items table and joining them with the categories and suppliers tables to get the category and supplier names. He’s also filtering items with prices greater than 100 and 
ordering them by item name.

Now I assisted him in optimizing the query by instructing him to select him few columns(items.id, items.name, items.price)  instead of all (items.*). We also added pagination to limit the number of rows returned by the 
query to improve the performance. However, the pagination doesn't help much because it's not a large dataset. I told him it's a better practice to include pagination. The resulting query looks like this  

				SELECT items.id, items.name, items.price*, categories.name AS category_name, suppliers.name AS supplier_name
				FROM items
				JOIN categories ON items.category_id = categories.id
				JOIN suppliers ON items.supplier_id = suppliers.id
				WHERE items.price > 100
				ORDER BY items.name
				LIMIT 10 OFFSET 20;

In the end, we improved the page load times by optimizing the query to select only the necessary columns and implementing the pagination.
