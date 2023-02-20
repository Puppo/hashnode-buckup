# Why I love GitLens in my VsCode - Part 2

When you work with git, you want to get info about commits and who changed the codebase quickly.  
  
With GitLens, you can get much info about your current file without loose focus on it. First, at the top of your file, you can get info about the last change and the name of the person who pushed that commit. In addition, there is also the info on the number of people that had touched the file.

![Info at top of the file](https://cdn.hashnode.com/res/hashnode/image/upload/v1676888540974/b6a0ec97-63da-44f5-8944-4421cb88e95a.png align="center")

This information is clickable. You can click on the part relative to the last commit or the other one.  
The first part opens the VsCode command with some possible actions to see the commit; you can see all the files relative to the commit, open the commit detail, and see the commit in the commit-graph. This is very helpful if you want to get info quickly about the changes in the file.  

![Result on click in the last commit](https://cdn.hashnode.com/res/hashnode/image/upload/v1676889210648/61e03949-5891-4fa9-b537-89a1af3a79d9.png align="center")

Instead, If you click on the second part (that is relative to the other authors of the file), GitLens opens a new bar on the left of the file and shows, for each line, the last commit relative to it, so you can understand who and why someone has changed the line.

![Blame bar](https://cdn.hashnode.com/res/hashnode/image/upload/v1676889388275/ffa12d59-9456-41f5-a386-88cb9f6d010b.png align="center")

This view is also available using the icon with the git logo in the top right of the file, and you can toggle this view by clicking it easier.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1676889590594/8b474581-1fef-44eb-8e28-fde6061adbb9.png align="center")

All these features are fantastic, but something we need more, for instance, searching for a commit or comparing two different commits.  
To do that, in the GitLens bar, you can find an option called "Search & Compare".  

![Search & Compare](https://cdn.hashnode.com/res/hashnode/image/upload/v1676890305693/a237b1f8-8ac5-4360-8901-01e6224cc217.png align="center")

Let's start with the search feature. Using this feature, you can search for a commit by different filters: commit message, author, SHA, file or changes. Typically, in my case, I use this feature to find an old commit by message or by author. The feature is very straightforward. If you click the button, the extension opens a command with different options; you can select your choice and type your terms. After that, in the GitLens panel will appear the results of the search.  

![Commit Search](https://cdn.hashnode.com/res/hashnode/image/upload/v1676892312451/5a4640a9-3f11-401b-b458-63f2751cb331.png align="center")

![Search result](https://cdn.hashnode.com/res/hashnode/image/upload/v1676892324327/99fd4f55-6074-400e-9d7d-af6f41eb4f8c.png align="center")

With this view, you can check the commits and see the files changed in those commits.  
  
After the search could be necessary to compare two commits, you can use the other button called "Compare references" to do that.  
Also, this feature is easy to use. Clicking the button "Compare References" appears a new VsCode command, where you can type the reference of your branches/tags or commits. Obviously, you have to indicate two references for the comparison.

![Compare references](https://cdn.hashnode.com/res/hashnode/image/upload/v1676893376968/36cf6c46-dc2d-4dbf-8ca3-bc185e3ac870.png align="center")

For me, this is really convenient when I have to compare two different versions of the code in the past or to check when and why I piece of the code has changed.

  
Ok, that's all folk.  
I hope you have other tips for improving your productivity with git using GitLens.  
  
Let me know if you know these features feature and if you think they are or could be helpful to you too.

See you soon folks

Bye bye 👋  
  
*If you are interested in it, use my referral* [***link***](https://www.gitkraken.com/invite/whbhwrJL) *to try GitLens or other GitKraken products for Free!* [***gitkraken.com/invite/whbhwrJL***](http://gitkraken.com/invite/whbhwrJL)