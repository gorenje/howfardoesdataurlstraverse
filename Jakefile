/*
 * Jakefile
 * howfardoesdataurlstraverse
 *
 * Created by You on March 23, 2011.
 * Copyright 2011, Your Company All rights reserved.
 */

var ENV = require("system").env,
    FILE = require("file"),
    JAKE = require("jake"),
    task = JAKE.task,
    FileList = JAKE.FileList,
    app = require("cappuccino/jake").app,
    configuration = ENV["CONFIG"] || ENV["CONFIGURATION"] || ENV["c"] || "Debug",
    OS = require("os");

app ("howfardoesdataurlstraverse", function(task)
{
    task.setBuildIntermediatesPath(FILE.join("Build", "howfardoesdataurlstraverse.build", configuration));
    task.setBuildPath(FILE.join("Build", configuration));

    task.setProductName("howfardoesdataurlstraverse");
    task.setIdentifier("com.yourcompany.howfardoesdataurlstraverse");
    task.setVersion("1.0");
    task.setAuthor("Your Company");
    task.setEmail("feedback @nospam@ yourcompany.com");
    task.setSummary("howfardoesdataurlstraverse");
    task.setSources((new FileList("**/*.j")).exclude(FILE.join("Build", "**")));
    task.setResources(new FileList("Resources/**/**"));
    task.setIndexFilePath("index.html");
    task.setInfoPlistPath("Info.plist");

    if (configuration === "Debug")
        task.setCompilerFlags("-DDEBUG -g");
    else
        task.setCompilerFlags("-O");
});

task ("default", ["howfardoesdataurlstraverse"], function()
{
    printResults(configuration);
});

task ("build", ["default"]);

task ("debug", function()
{
    ENV["CONFIGURATION"] = "Debug";
    JAKE.subjake(["."], "build", ENV);
});

task ("release", function()
{
    ENV["CONFIGURATION"] = "Release";
    JAKE.subjake(["."], "build", ENV);
});

task ("run", ["debug"], function()
{
    OS.system(["open", FILE.join("Build", "Debug", "howfardoesdataurlstraverse", "index.html")]);
});

task ("run-release", ["release"], function()
{
    OS.system(["open", FILE.join("Build", "Release", "howfardoesdataurlstraverse", "index.html")]);
});

task ("deploy", ["release"], function()
{
    FILE.mkdirs(FILE.join("Build", "Deployment", "howfardoesdataurlstraverse"));
    OS.system(["press", "-f", FILE.join("Build", "Release", "howfardoesdataurlstraverse"), FILE.join("Build", "Deployment", "howfardoesdataurlstraverse")]);
    printResults("Deployment")
});

task ("desktop", ["release"], function()
{
    FILE.mkdirs(FILE.join("Build", "Desktop", "howfardoesdataurlstraverse"));
    require("cappuccino/nativehost").buildNativeHost(FILE.join("Build", "Release", "howfardoesdataurlstraverse"), FILE.join("Build", "Desktop", "howfardoesdataurlstraverse", "howfardoesdataurlstraverse.app"));
    printResults("Desktop")
});

task ("run-desktop", ["desktop"], function()
{
    OS.system([FILE.join("Build", "Desktop", "howfardoesdataurlstraverse", "howfardoesdataurlstraverse.app", "Contents", "MacOS", "NativeHost"), "-i"]);
});

function printResults(configuration)
{
    print("----------------------------");
    print(configuration+" app built at path: "+FILE.join("Build", configuration, "howfardoesdataurlstraverse"));
    print("----------------------------");
}
