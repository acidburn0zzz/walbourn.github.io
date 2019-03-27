---
layout: msdnpost
title: DXSETUP Update
date: 2011-04-19 10:49
author: Chuck Walbourn
comments: true
categories: [directx, dxsdk]
---
As I noted in my post on a <a href="https://walbourn.github.io/dxwebsetup-update/">DXWSETUP</a> back in November 2010, we have addressed a number of bugs in DirectSetup after the release of the DirectX SDK (June 2010). These bugs include some localization display issues with the EULA and various non-Codepage 1252 languages, plus resolving a problem with .NET 4.0's strong deprecation of <code>GetCORVersion</code> function used to detect which version of .NET (if any) is present on the system. Even without the legacy Managed DirectX 1.1 CABs present, this check triggers a non-fatal error pop-up on systems with only the .NET 4.0 Runtime installed. As noted before, this does not impact Windows Vista, Windows 7, Windows Server 2008, or Windows Server 2008 R2 machines which always include the .NET 2.0, 3.0, or 3.5 runtime. It doesn't impact most existing Windows XP systems since most have either no .NET runtime installed or some version of .NET 2.0, 3.0, or 3.5. This also includes the change for an improved error message when run on Windows XP RTM, Windows XP SP1, or Windows Server 2003 RTM machines (which are not supported scenarios, but the original June 2010 release of DirectSetup generates an obscure error message in this case).
<!--more-->

Since most usage of DXSETUP (the DirectX SDK REDIST folder) is with the <code>/silent</code>  switch, the localization fixes do not impact most publishers using DirectSetup to deploy their optional DirectX SDK side-by-side dependencies (D3DX9, D3DX10, D3DX11, D3DCSX, D3DCompiler, XINPUT, XAUDIO2, XACTENGINE, and/or X3DAUDIO). With the strong deprecation of <code>GetCORVersion</code> with .NET 4.0, we are seeing some publishers concerned about the error pop-up that occurs on "fresh" Windows XP deployments with only the .NET 4.0 runtime installed even with <code>/silent</code>. To address those concerns we have refreshed the <a href="http://www.microsoft.com/downloads/en/details.aspx?displaylang=en&FamilyID=3b170b25-abab-4bc3-ae91-50ceb6d8fa8d" title="DirectX End-User Runtimes (June 2010) [MS Downloads]">DirectX End-User Runtimes (June 2010)</a> stand-alone installer (which now has a published date of 4/18/2011), which is essentially just a ZIP'd version of the DirectX SDK REDIST folder. <em>None of the REDIST CABs or the DLLs it deploys have changed from their June 2010 versions. This only modifies the DirectSetup files themselves, notably <code>dsetup.dll</code>, <code>dsetup32.dll</code>, <code>dxdllreg_x86.cab</code>, <code>dxsetup.exe</code>, and <code>dxupdate.cab</code> </em>. These refreshed files are subject to the same EULA as present in the DirectX SDK (June 2010) release, and can therefore be redistributed with your application if desired.

Anyone working with DirectSetup or DirectX application deployment should be sure to review my <a href="https://walbourn.github.io/not-so-direct-setup/">blog post</a> on the subject, as well as the various linked articles.

In addition to a refresh of the stand-alone installer, we have again updated the <a href="http://www.microsoft.com/downloads/en/details.aspx?FamilyID=2da43d38-db71-4c1b-bc6a-9b6652cd92a3" title="DirectX End-User Runtime Web Installer [MS Downloads]">DirectX End-User Runtime Web Installer</a> (which now has a published date of 4/18/2011) for the Bing Bar version 7 release. There are no other changes to the web installer beyond those described in my previous <a href="https://walbourn.github.io/dxwebsetup-update/" title="DXWEBSETUP Update">blog post</a>. <strong><em>The Bing Bar offer is limited to only the Web Installer. The stand-alone installer does not offer nor does it install the Bing Bar</em>.</strong>

<strong>Update:</strong> Note that Windows 8.x and Windows 10 include the .NET 4.5 Runtime. The .NET 3.5 Runtime can be optionally enabled, but is not present by default. Therefore, these Windows 8.x and Windows 10 systems trigger a "Windows Feature" request dialog if it has not already been enabled. This refreshed version of DXSETUP and DXWSETUP both resolve this issue for the Windows 8.x and Windows 10 as well.

There are no plans to update this package for newer releases of D3DCSX or D3DCompiler. These are only available in the Windows 8.0 SDK, Windows 8.1 SDK, and/or Windows 10 SDK.

<strong>FCIV:</strong> The best way to validate that you have an uncorrupted copy of this package it to run <code><a href="http://support.microsoft.com/kb/841290">fciv</a> -sha1 directx_Jun10_redist.exe</code> and verify you get <code>f8f1217f666bf2f6863631a7d5e5fb3a8d1542df directx_jun2010_redist.exe</code>