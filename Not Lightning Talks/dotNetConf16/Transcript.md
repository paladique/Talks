#A Lap around Octokit.NET

Octokit.NET is a Client library for GitHub API, written in C#, that helps .NET devs write apps that interact with the Github API. What you'd essentially use the API for is for making custom tools that integrate with GitHub and your workflow. And of course, you could also just make something just for fun.

So some features about the library is that it has some access to numerous platforms, including .NET 4.5, Xamairin, Mono, [[1](https://github.com/octokit/octokit.net#supported-platforms)] so a diverse set of platforms to try and play with. Also, it's available on NuGet.Installing Octokt.NET is pretty straightforward, it shouldn't take long as its dependencies are things that you probably already have (like .NET 4.5 and System.Net.HTTP) [[2](https://www.nuget.org/packages/Octokit/0.1.3)]

So let's move on to the topic of of how Octokit work with GitHub's API. So version 3.0 of the GitHubAPI is a RESTful API that also supports authentication, specifically OAuth. It sends and recieves JSON and Octokit.NET desrializes these responses into a simple and intuitively written and easy to use library that are mapped onto Types that are synonmous with the API's endpoints. For example, in the API if I wanted to return all of the issues in a repo then I'd find it in the API documentation and put in the url, but this is what it looks like in Octokit.

So just a little aside to the deserialization let's look at how octokit actually does it, Octokit uses SimpleJSON   (SimpleJsonSerializer.cs) [[4](https://github.com/octokit/octokit.net/blob/f354d1bf00ff7606b46489e3a915e1428414bc47/Octokit/Http/SimpleJsonSerializer.cs)] library to set this up for you. One reason for this is it makes it easier for you, the developer, to not have to worry about things like attributes that are written in ruby conventions, which you're probably not used to as a .NET dev.

One great way to start using Octokit is to look at the integration tests. [[5](https://github.com/octokit/octokit.net/tree/master/Octokit.Tests.Integration/Clients)] Let's do that now and see what's going on in there.
This is test is doing x
this test is doing y


So how do you get started?

After grabbing it on NuGet, the first thing you'll probably wanna do is set up the GitHubClient [[6](https://github.com/octokit/octokit.net#usage-examples)], put your app name in there which is your User Agent (we'll get to that soon). After they you're all set to play around with the API.

First we're gonna make a GET request by grabbing some repos and print them to my console app so I'll make a repository object and grab all my public repos. We've gotta make a task to do this because in the event you've got a big ol list of repos it might take a while. And Octokit forces you to do this anyway. And there we are!

Next, let's do a POST by rendering some markdown. I've made a Web Form project that has a textbox that I'm gonna write my markdown into, when I press the button it's gonna render it into the lable I put into here.

GitHub's API supports OAuth Web Application flow, so you can authenticate through GitHub without asking for the user's credentials. [[7](http://octokitnet.readthedocs.io/en/latest/oauth-flow/)] Let's take a look at how it works. When I visit, it's going to prompt me to reject or accept the authentication request. I say yes, and see all the repos.

Some things to be mindful of when making your first project in Octokit is your rate limit, you can only make 60 requests per hour when unauthenticated, but 5000 when you are [[8](https://developer.github.com/v3/#rate-limiting)]. Also, make sure you have User Agent set, which is probably your app name that you put as string parameter in the product header value when you make the client, or else you'll get rejected from the API (401).[[9](https://developer.github.com/v3/#user-agent-required)]. Finally, consider checking the status of the API through your app and putting in error handling in there in the event there's a problem accessing GitHub. [[10](https://status.github.com/api)]

A few features that might be of interest to is:

- Pagination
  - By default Octokit returns the whole data set of a request, but with a ApiOptions instance you can control what is returned.[11](http://octokitnet.readthedocs.io/en/latest/extensibility/#pagination)     
- Symbol debugging
  -Step into Octokit via your project
  -Options > General > Enable source server support [](http://octokitnet.readthedocs.io/en/latest/debugging-source/)
- Enterprise support
  - Custom tool solutions for on-premise repos
- Reactive extension support 
  - IObservable library for use with Reactive Extensions
      - Octonotes, written by maintainer
      - GitHub for VS Extension


Octokit is open source and you can check out what's going on their repo and make some contributions. Consider taking on some of the issues marked upforgrabs and making a pull request off that issue with your ennhancements or fixes. Don't forget to make some tests! How it normally works is that a maintainer will review your code and make comments on it and when if your build is passing and it looks good they'll merge it! Check out issues and  for discussions on features, for example there's a really involved discussion about core support going on at the moment.[[12](https://github.com/octokit/octokit.net/issues/1115)]


##Footnotes and additional references
** Repo examples available in C#, VB.NET, and F#

** Contect me me at [@paladique](https://twitter.com/paladique) for questions or check out the [Octokit.NET](https://github.com/octokit/octokit.net) repo where one of the maintainers can answer qs or search the Issues to see if it's been answered.

** Gif from Before you Build is image of Scar from [The Lion King](https://en.wikipedia.org/wiki/The_Lion_King), scene is musical number calles ("Be Prepared")[https://en.wikipedia.org/wiki/Be_Prepared_(song)] when he plans to take over the kingdom of Pride Rock.

[Slide Design Credits](http://www.slidescarnival.com/jourdain-free-presentation-template/403)

[@evilpaladique's picture source](https://ericandrewlewis.github.io/emoji-mosaic/)
