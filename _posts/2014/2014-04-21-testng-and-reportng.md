---
layout: post
title: TestNG and ReportNG
categories: testing
tags: 
- TestNG
- ReportNG
---
TestNG and ReportNG

## Ant
    <testng classpathref="test-path"
          outputdir="${test-results.dir}"
          haltonfailure="true"
          useDefaultListeners="false"
          listeners="org.uncommons.reportng.HTMLReporter">
    <xmlfileset dir="." includes="testng.xml"/>
    <sysproperty key="org.uncommons.reportng.title" value="My Test Report"/>
    </testng>


## Java Main
    public static void main(String[] args) {
        TestNG testng = new TestNG();
        testng.setUseDefaultListeners(false);
        List<String> suites = new ArrayList<String>();
        suites.add("F:/Mhj/ReportNg/testng.xml");
        
        testng.setTestSuites(suites);
        testng.run();
    }

## reportng
\org\uncommons\reportng\messages\reportng.properties
\org\uncommons\reportng\templates\html
    results.html.vm
    class-results.html.vm
    reportng.css