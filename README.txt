VDO 2020/03/13
The Command and Query Responsibility Segregation (CQRS) <-- for the flair codes/org, etc, break this down. So the API will only return info. 
The actual management will be in the blazor app.

VDO 2020/03/05

TODO: https://stackoverflow.com/questions/59256798/how-to-use-bootstrap-modal-in-blazor-client-app
Where do I put css files and include them? They are in the css folder moron
https://chrissainty.com/get-some-sass-into-your-blazor-app/
https://docs.microsoft.com/en-us/dotnet/architecture/blazor-for-web-forms-developers/project-structure

Extensions -> Manage Extension -> Git hub and Web Compiler

VDO 2020/02/20

Is it better to query async or Task.Run(() => query none async) ??

Make sure you have EF reference/using in the service and toListAsync. TADA!

        //https://docs.microsoft.com/en-us/dotnet/api/microsoft.entityframeworkcore.entityframeworkqueryableextensions.tolistasync?view=efcore-3.1
        //https://stackoverflow.com/questions/26676563/entity-framework-queryable-async



VDO 2020/02/07
What I learned:
Blazor components must be created (you can't rename) with a capital letter
Don't add Razor, it will be old pages not BLAZOR components
@Page "/" is what sets the start page. Don't remove it from Index
@page "/vcscomponent" is what tell routing the path. So the componet and path are now no longer related. Of course
Componets are build, you can't refresh. Crap


VDO 2020/01/24
SOOOO
Since the repository manager and UOW are working off of different DBContext..is that the reason it isn't picking up the new entity? In this case the UOW will have to be injected into the service. 
Shit.

IT WORKS!
But the new entities auditing doesnt work
and is my USING working?
SELECT 
    DB_NAME(dbid) as DBName, 
    COUNT(dbid) as NumberOfConnections,
    loginame as LoginName
FROM
    sys.sysprocesses
WHERE 
    dbid > 0
GROUP BY 
    dbid, loginame

VDO 2020/01/21
Since the creation of the repository manager, we no longer have to inject the UOW into the services. yay!
Just inject it and let the UOW control the transaction and saving like it is supposed to do. Now the serices will not know the bounds of the request

VDO 2020/01/15 TODO
So..
Do I pass just the connection string to the UOW or the full? If that is the case, the controller would have to know  the DbContextOptionsBuilder<ScemsDBContext> optionsBuilder

I think the job of the factory would be take the connection string
Build the UOW
The IUnitOfWork would be in the using statement at controller/request level. The services would still have them injected so the save would work. 
The commit and roll back in the controller level

SO factory takes connection string, builds UOW, builds servies? Hm???
But a factory can create other services that do not rely on connection strings
So should it only be EntityServiceFactories takes a connection string? 

But if the factory builds the UOW, how would it know which one, real or shim?

So not only do you have to add the EFcore package, but it needs to know the provider also:
Microsoft.EntityFrameworkCore.SqlServer
https://docs.microsoft.com/en-us/ef/core/providers/index?tabs=dotnet-core-cli



SOOO if the UoW manager and EntityService factory are in the base controller that should hide a lot of stuff. (as protected)



