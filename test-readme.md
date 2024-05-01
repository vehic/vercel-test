1. From this [list](https://gist.github.com/Pieparker/b04a4e9ff82ba949e5db9d5b0e9d89e8), rank your 5 most favourite and 5 least favourite support tasks. Provide a brief explanation for each.

Ans -> Below are my 5 most favourite support tasks:

  * Dig through logs to troubleshoot a customer's broken project -- It's a challange that every support engineer had to go through every day and once it is solved, it gives satisfaction.
  * Write and maintain support articles and docs pages -- Makes interal team life easy because if support docs are upto date then you don't habe to depend on anyone, follow the doc and do 
    your work.
  * Create video tutorials to help teach users a specific feature or use case -- Video tutorials are helpful for end users, then can simply watch the video and learn how to use the 
    platform, it will reduce the support dependecy and support engineers could work on other important things.
  * Work with the product team to develop a new feature based on feedback from customers -- Customers feedback are important to build a better product, not all feedback are considered but 
    even if out of 10 one or two feedback is correctly processed we can build a better product and customer would also feel heard.
  * Help train and onboard new support teammates -- Sharing the already gained knowledge about the product would enhnace my skill set.


  Below are my 5 most favourite support tasks:
  
  * Help resolve billing issues for customers -- I think for billing issues there should be other teams available to handel them, support engineers should be more focused on solving 
    techical issues.
  * Respond to queries on Twitter, Reddit, Hacker News and other 3rd party sites -- Social support is somewhere you cannot solve all the issues neither you can share your troubleshooting 
    steps nor you can ask them for internal information needed for troubleshooting, at last you would have to route them through support tickets.  
  * Engage multiple users at once in a public discussion, to answer their questions and troubleshoot problems -- If this has to be done once in a while then I'm good with it, but not 
    everyday.
  * Respond to 50+ support requests via email every day -- I feel this much volume will make burden everday
  * Manage a support team -- As of now I feel more comfortable as individual contributor. 

---

2. What do you want to learn or do more of at work?

Ans -> As a technical support engineer, I'm eager to deepen my understanding of our products and services, particularly in areas where I can enhance my troubleshooting skills and provide even more effective solutions to our customers. I'm also keen on expanding my knowledge of emerging technologies relevant to our industry. This not only allows me to grow professionally but also enables me to better support our team by sharing insights and best practices. I'm excited about opportunities to expand my knowledge and skills in this role.

---

3. Describe how you solved a challenge or technical issue that you faced in a previous role (preferably in a previous support role). How did you determine that your solution was
successful?

Ans -> 
**Issue:** Sign in for the first time or re-auth through Okta, user's are getting stuck on a blank screen for 20-30 seconds.  It's really not a very good user experience.

**Troubleshooting Steps:**
* Asked to screen record the issue and send the recording to us. Asked some more question to help me investigate further:
1. What device, browser, and browser version are they using?
2. If their browser version needs to be updated, can they update then try to reproduce the issue?
3. Does this issue happen on other browsers?

Also, asked the, generate and share a HAR file while reproducing this issue? (Steps can be found here https://support.zendesk.com/hc/en-us/articles/4408828867098-Generating-a-HAR-file-for-troubleshooting-)

* Once, I had all the information I reviwed the screen recording and analyzed the HAR file using [Google HAR Analyzer](https://toolbox.googleapps.com/apps/har_analyzer/) and found that two of the endpoints are taking much longer tine than expected.
https://xyz/api/v1/config
wss://xyzm-websocket-a.playit.io

* In order to confirm this situation, I tried to login using the same flow and genrated the HAR file from my test account and then compared both the file side by side and checked for those 2 endpoints and confirmed that for me those 2 endpoints are not taking much in comparison to customers.

* After further checking debug logs found that config file takes longer to render intialy as the config file has more than 50k lines of code due to having many sources and when user logs in for the first time the config file renders first. Since, config file is big it is slowing the login process.

* Quick Fix Solution : Made the changes in code to skip private auth for same sources, instead of using authentication multiple times for similar sources, now we will only authnticate once and then mapp the auth to other similar sources. This reduced the waiting time significantly.

* Rasised the PR for the changes and confirmed from Engineering and informed customer once the PR was deployed on next release.

My Solution was successful because customer wanted the fix before their release and we had hard stop, So the quick fix which I applied reduced the waiting time. However, engg team took over to make it standard process for all accounts later on.


---

4. When would you choose to use Edge Functions, Serverless Functions, or Edge Middleware with Vercel?

Ans -> Serverless Functions: Gives you access to all the Node.js APIs that you would expect for writing on the web, with the ability to configure machine resources and dependencies.
Edge Functions: Opt for this cost-effective choice when you need lightweight JavaScript functions that execute close to the user

I would choose Edge Functions for manipulating HTTP traffic at the edge, Serverless Functions for handling dynamic server-side logic, and Edge Middleware for applying common functionality across multiple routes or pages.

---

5. Imagine a customer writes in requesting help with a build issue on a framework or technology that you've not seen before. How would you begin troubleshooting this and what questions would you ask the customer to understand the situation better?

Ans -> I will start with gathering initial information:
* Request details about the specific error message encountered during the build process. Based on the error message I will check Logs to find more information about the issue.
* Get details about the framework or technology they are using and the version numbers involved along with recent changes or updates made to the project or development environment that might have triggered the issue.

Review the documentation and previous support cases:
* Review the framework or technology in question to understand its build process, common issues, and troubleshooting steps.
* Check the official documentation, community forums, and online resources for insights and potential solutions. Also look into previous support cases and threads.

Try to replicate the issue:
* Try to reproduce the problem on my end using the information provided by the customer.
* Set up a similar development environment, including the same framework or technology version, dependencies, and configurations.

Isolate the Problem:
* Narrow down the scope of the issue by testing different components or stages of the build process.
* Determine if the problem is related to a specific configuration setting, dependency, script, or environment variable.

Work towards finding solutions:
* Propose potential troubleshooting steps or workarounds based on my understanding of similar issues or best practices.
*  Check with other team members regarding this issue, if required would take help from engineering team.

---

6. The customer from question 5 replies to your response with the below:
      
“I’m so frustrated. I’ve been trying to make this work for hours and I just can’t figure it out. It must be a platform issue so just fix it for me instead of asking me questions.”
Please write a follow-up reply to the customer.

Ans -> I would format my response in below manner

    Hi There,
    
    Thank you for reaching out to Vercel Support. I completely understand your frustration, and I'm truly sorry for the difficulties you've encountered while trying to resolve this issue. 
    I can imagine how frustrating it must be to spend hours grappling with a problem without making headway.

    While I appreciate your concern that it may be a platform issue, it's essential for us to gather as much information as we can to diagnose the problem accurately. Every project and 
    environment can have unique configurations and dependencies that may contribute to the issue.

    I'm here to support you every step of the way. If you could provide any error messages or logs that you've encountered during your attempts, it would greatly assist us in diagnosing 
    the root cause of the issue. Once we have a better understanding of the problem, I'll work diligently with our team to find a resolution on this issue. 

    Rest assured, I'm committed to assisting you until we get this resolved. Thank you for your patience and cooperation.

    Best Regards
    Timus

---


7. A customer writes in to the Helpdesk asking "How do I do a redirect from the /blog path to https://example.com?" Please write a reply to the customer. Feel free to add any information about your decision making process after the reply.

Ans -> 

    Hi There,

    Thank you for reaching out to Vercel support. My name is Timus and I'd be more than happy to help you.
    
    To achieve this redirection with Vercel, you can utilize Vercel's routing configuration in your project's vercel.json file. Here's how you can set up the redirect:

    {
    "redirects": [
    
    { "source": "/blog", "destination": "https://example.com", "statusCode": 301 }
      ]
    }

    I have shared some helpful links that would provide you more information on this issue:
    https://vercel.com/docs/edge-network/redirects
    https://medium.com/@kaushikwrites/how-to-redirect-nextjs-website-blog-deployed-on-vercel-to-wordpress-blog-210f6b56111f
    
    With this configuration, any requests made to "/blog" will be redirected to "https://example.com" with a permanent (301) redirect status.

    Once you've added this redirection rule to your vercel.json file, deploy your project to Vercel, and the redirection should take effect.

    If you have any further questions or need assistance with this setup, please feel free to let me know, and I'll be happy to help!

    Best regards,
    Timus

 Decision making process:    
 I have recommend using the vercel.json configuration for redirects because it allows you to manage redirects at the edge, making them faster and reducing load on your origin server. This 
 method is simple to implement and manage directly within your codebase, keeping all configurations version-controlled and transparent. Also, handling redirects through vercel.json makes 
 it easy to adjust or add new redirects in the future without needing to alter server configurations or deploy code changes. It provides a centralized, scalable approach to manage routing 
 rules, which is ideal for performance and ease of maintenance.


---

8. A customer is creating a site and would like their project not to be indexed by search engines. Please write a reply to the customer. Feel free to add any information about
your decision making process after the reply.

Ans ->

    Hi There,

    Thank you for reaching out to Vercel support. My name is Timus and I'd be more than happy to help you.

    In order to skip indexing your projects by search engines you would have to insert a noindex meta tag in the <head> section of each HTML page you want to exclude from search engines. 
    This tag is more reliable than robots.txt for preventing indexing because it directly tells any compliant search engine not to index the page:
    <meta name="robots" content="noindex">
    This needs to be added to each page individually, or dynamically if you're using a web framework or CMS that allows for programmatic header management.

    You can get more information through this link https://github.com/orgs/vercel/discussions/1060.

    Please ensure that these changes are added correctly to avoid any unintended indexing. If you have multiple pages or a dynamic site and need a more scalable solution, or if you have 
    any specific setup or questions, feel free to let me know. I'm here to help!

    Best regards,
    Timus

Decision making process: 
I have provided the option of noindex instead of robots.txt file because robots.txt file method relies on the voluntary cooperation of the search engine bots, and it doesn't completely guarantee that pages won't be indexed, especially if there are external links pointing to them.

---


9. What do you think is one of the most common problems which customers ask Vercel for help with? How would you help customers to overcome common problems, short-term and long-term?

Ans -> Vercel is a platform designed to optimize the development and deployment of front-end and serverless applications. It specifically targets challenges related to modern web development, such as performance optimization, scalability, and developer productivity. Here are some key problems that Vercel addresses:

* **Problem:** Traditionally, deploying web applications can be cumbersome, requiring setup, configuration, and management of servers, environments, and deployment processes.

**Vercel’s Solution:** Vercel automates much of this process, enabling developers to deploy sites and applications by simply pushing their code to a Git repository. This eliminates the need for manual server setup and configuration.

* **Problem:** Ensuring high performance across global locations can be challenging and resource-intensive, often requiring complex CDN setups and optimizations.

**Vercel’s Solution:** Vercel automatically optimizes web applications by serving them from a global Content Delivery Network (CDN), reducing latency by serving content from data centers close to the user. It also optimizes images and static files automatically.

* **Problem:** Scaling applications to handle increased traffic can be difficult, especially when dealing with variable loads and global audiences.

**Vercel’s Solution:** Vercel provides automatic scaling without requiring manual intervention. Applications deployed on Vercel can effortlessly scale up during traffic spikes and scale down during quieter periods, ensuring efficiency and reducing costs.

* **Problem:** Developers often spend significant time configuring environments, which can detract from time spent on actual development.

**Vercel’s Solution:** Vercel enhances developer productivity through its seamless integration with development tools and workflows, particularly for frameworks like Next.js. Features like instant previews, automatic deployments, and integration with popular development tools and services streamline development processes.

Short-Term Solutions
Immediate Assistance and Troubleshooting:

* Review Logs and Error Messages: Encourage customers to carefully review build logs and error messages. These often provide crucial clues about what might be going wrong.
* Check Configuration Files: Ensure vercel.json and other project configuration files are set up correctly according to the needs of the project and Vercel's documentation.
* Validate Environment Variables: Misconfigured or missing environment variables can often cause deployments to fail. Ensuring these are correctly set for different environments (development, production) can resolve many issues.

Long-Term Solutions
Education and Resources:

* Comprehensive Documentation: Continuously update and improve the documentation to cover common pitfalls, configuration options, and best practices.
* Community and Support: Foster a strong community around Vercel where developers can share their experiences, solutions, and best practices. This can be through forums, chat groups, or regular community calls.
* Feedback Loops: Implement effective feedback loops where user problems and their solutions are regularly analyzed to improve the platform and its usability.

---

10. How could we improve or alter this familiarisation exercise?

Ans -> I would suggest to give more hand's on task on vercel rather than writing answers. If there would be tasks to be done on vercel than candidate would be more familarise with the platform and it would be more easy to understand what product does and how it works.

    
