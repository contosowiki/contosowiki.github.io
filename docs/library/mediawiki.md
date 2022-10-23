---
layout: default
title: MediaWiki
parent: Library
nav_order: 2
---

# MediaWiki
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## About MediaWiki

MediaWiki helps you collect and organize knowledge and make it available to people. It's powerful, multilingual, free and open, extensible, customizable, reliable, and free of charge.

https://www.mediawiki.org

## MediaWiki skin - Foreground

Foreground is a MediaWiki skin that puts your content front and center!

https://foreground.wikiproject.net

## Foreground Demo

MediaWiki:Common.css
```css
/* CSS placed here will be applied to all skins */
#siteSub {
    display: none;
}
#toc {
    /* Add opacity (translucency) */
    background-color: rgb(249, 249, 249);
    background-color: rgba(249, 249, 249, 0.7); /* Higher opacity (last arg) means less transparency */
}
#t-whatlinkshere { display: none; }
#t-recentchangeslinked { display: none; }
#t-specialpages { display: none; }
#t-permalink { display: none; }
#t-info { display: none; }
/* footer */
#footer-lastmod { display: none; }
#footer-privacy { display: none; }
#footer-disclaimer { display: none; }
.mw-highlight pre {
	font-family: "Courier New", monospace;
	font-size: 100%;
	background: #eaecf0;
	line-height: 150%;
	margin-top: .5em;
	margin-bottom: 1em;
	width: auto;
	padding-top: 8px;
	padding-left: 10px;
	padding-bottom: 10px;
	border-left: solid 0.3em;
	border-left-color: #32CD32;
	box-shadow: 5px 5px 5px #DCDCDC;
}

/* Below is from foreground */
.row.display {
	background: #eee;
	font-size: 11px;
	margin-bottom: 10px;
}
.row.display .columns,
.row.display .column {
	background: #e7e7e7;
	border: 1px solid #ddd;
	font-size: 13px;
	font-weight: bold;
	text-indent: 3px;
	padding-top: 8px;
	color: #444;
	padding-bottom: 8px;
}

/* make the reason selection for &action=protect bigger */
#mwProtect-level-edit,
#mwProtect-level-move {
	height: 65px;
}

/* CodeRay Syntax Highlighting Styles to match Github */
.CodeRay {
	background-color: #eee;
	border: 1px solid #ccc;
	font-family: "Consolas", "Liberation Mono", Courier, monospace;
	color: #000;
	padding: 0.8em 0 0.8em 0.8em;
 	margin-bottom: 1.3em;
	overflow: auto;
}

.CodeRay pre {
	margin: 0;
	font-size: .9em;
	line-height: 1.4em;
	white-space: pre;
}

/* CookieWarning */
.mw-cookiewarning-container {
	min-height: 4em;
	padding: 15px;
}

/* VisualEditor
 * fix for https://github.com/jthingelstad/foreground/issues/331
 */
.oo-ui-toolbar-bar .oo-ui-tool .oo-ui-tool-link {
	padding-top: 0
}
/* Image zooming */
	.geeks {
		float: left;
		overflow: hidden;
		margin-right: 10px;
	}
	.geeks img {
		width: 100%;
		height: 100%;
		transition: 0.5s all ease-in-out;
	}
	.geeks:hover img {
		transform: scale(1.1);
	}

```

MediaWiki.Common.js
```css
/* Any JavaScript here will be loaded for all users on every page load. */
/* 百度统计 */
var _hmt = _hmt || [];
(function() {
  var hm = document.createElement("script");
  hm.src = "https://hm.baidu.com/hm.js?xxxxxxxxx";
  var s = document.getElementsByTagName("script")[0]; 
  s.parentNode.insertBefore(hm, s);
})();

```

MediaWiki:Sidebar
```css
* Network
** Switch|Switch
** Router|Router
* vSphere
** ESXi|ESXi
** VM|Virtual Machine
** vCenter|vCenter
* Windows
** ADDS|Active Directory
** DHCP|DHCP
** File-Share|File Share
** Printing|Printing
** OSD|OS Deployment
* Linux
** Bash|Linux Command
** Linux-Service|Linux Service
** Linux-Script|Linux Script
* Backup
** Crashplan|Crashplan
** Acronis|Acronis
** Veeam|Veeam
* Monitor
** Zabbix|Zabbix
* Application
** Windows-Application|Windows Application
** Linux-Application|Linux Application
* SEARCH
```