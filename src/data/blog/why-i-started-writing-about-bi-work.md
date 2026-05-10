---
title: "Why I Started Writing About BI Work"
description: "After a decade in regulated-industry BI, I'm watching AI reshape the tools I've used every day. Here's why I decided to start writing about it."
pubDatetime: 2025-05-10T00:00:00Z
tags: ["bi", "tableau", "power-bi", "career", "ai-tools"]
draft: false
featured: true
---

> **DRAFT — review before publishing.**

I've spent over a decade building dashboards, tuning SQL, migrating reports between tools, and sitting in rooms explaining to business stakeholders why their numbers don't match. The work has been mostly invisible — not because it isn't valuable, but because good BI infrastructure tends to disappear into the background when it works.

That's starting to change.

## Why Now

The last year has been unusual. Tableau released its MCP server integration, which means language models can now query and generate Tableau content through a structured protocol. Power BI Copilot is showing up in enterprise licenses and letting analysts describe charts in plain English. Databricks is positioning dbt + Unity Catalog as the new standard for analytics engineering. And every vendor seems to have bolted "AI" onto something.

I've been watching this from the inside — managing a BI platform at GE Healthcare that spans 18 countries, running Tableau Server on AWS, reviewing GitLab PRs for a team of developers, and spending serious time debugging why a refresh failed at 3 AM in a market I've never visited.

The thing is: most of the AI-in-BI writing I've seen is written by people who haven't done production BI in a regulated environment. They haven't navigated row-level security for 500 users under AML compliance requirements. They haven't had to explain to a clinical lead in Germany why a dashboard number is different from what the device log says. They haven't owned a release cycle where a single bad calculation in a Tableau workbook could affect dosage compliance reporting across a hospital network.

I have. And I think that perspective is worth writing down.

## What I'm Going to Write About

Mostly practical things. When I test a new tool — say, connecting Claude to Tableau via MCP, or using Copilot to write a DAX measure I'd normally write by hand — I'll write about what actually happened, not what the marketing page promised.

I'll also write about fundamentals: data modeling choices that age well, SQL patterns for analytics workloads, how to structure a Tableau workbook that a future-you can actually maintain, why row-level security in Tableau Server is more nuanced than the documentation suggests.

And occasionally I'll write about the career side of BI — what it looks like to lead a cross-functional team through a production release, how to manage stakeholders in 18 different time zones, why "the data is wrong" is almost never a useful bug report.

## The Honest Version

I'm also writing because I want to get better at articulating what I know. After ten years of this, a lot of it lives in my fingers — in the muscle memory of spotting a context filter issue in a workbook, or knowing that a certain Redshift query plan means I should restructure the join order. Writing forces precision.

If some of it is useful to someone building their first Tableau Server deployment, or trying to understand whether Power BI Copilot is actually production-ready, or navigating their first AML compliance BI project — that's good enough.

Let's see where this goes.
