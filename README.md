# codePath

# Project 7 - WordPress Pentesting

Time spent: **5** hours spent in total

> Objective: Find, analyze, recreate, and document **five vulnerabilities** affecting an old version of WordPress

## Pentesting Report

1. (Required) Unauthenticated Stored Cross-Site Scripting (XSS)
  - [ ] Summary: JavaScript can be injected in WordPress comments due to large length of comment since MySQL Text has limited size of 64 kilobytes.
    - Vulnerability types: XSS
    - Tested in version: 4.2
    - Fixed in version: 4.2.1
  - [ ] GIF Walkthrough: <img src="https://imgur.com/a/uHhhI" width="800">
  - [ ] Steps to recreate: Go to comment section of one of the posts in WordPress, then leave the comment '<a title='x onmouseover=alert(unescape(/hello%20world/.source)) style=position:absolute;left:0;top:0;width:5000px;height:5000px  COMMENT HERE'></a>' where the comment has to be greater than or equal to 64 kb. Once you have posted this the exploit will show up.
  - [ ] Affected source code:
    - [Link 1](https://core.trac.wordpress.org/browser/tags/4.9/src/wp-includes/class-wp-comment.php#L15)
2. (Required) Legacy Theme Preview Cross-Site Scripting (XSS)
  - [ ] Summary: When the administrator previews a theme then "preview_theme_ob_filter_callback" removes the "onclick" handlers which will allow for an alert to pop up from the injected JavaScript within the comments. The GIF assumes that the administrator has already previewed the theme. The JavaScript being shown within the comments show the result of previewing theme since the "onclick" part of the injection is missing.
    - Vulnerability types: XSS
    - Tested in version: 4.2.3
    - Fixed in version: 4.2.4
  - [ ] GIF Walkthrough: <img src="https://imgur.com/a/v73oq?" width="800">
  - [ ] Steps to recreate: Administrator previews a theme on WordPress allowing for the removal of the onclick handler in the comment section of a post. A comment may now be posted as follows: <a href='/wp-admin/' title="" style="position:absolute;top:0;left:0;width:100%;height:100%;display:block;" onmouseover=alert(1)//'>Test</a>. Because of the preview of the theme the onclick handler has been removed this all happened.
  - [ ] Affected source code:
    - [Link 1](https://core.trac.wordpress.org/browser/tags/4.9/src/wp-includes/deprecated.php#L3473)
3. (Required) Large File Upload Error XSS
  - [ ] Summary: When an Administrator uploads an image file that is too large to be uploaded, then if the name of the image file contains executable JavaScript, it will be run.
    - Vulnerability types: XSS
    - Tested in version: 4.7.4
    - Fixed in version: 4.7.5
  - [ ] GIF Walkthrough: <img src="https://imgur.com/a/DMuEh" width="800">
  - [ ] Steps to recreate: Create an image file that is ~20 MB large and name it some text with <img src=x onerror=alert(1)>. Upload this file at http://wpdistillery.vm/wp-admin/media-new.php and the alert should pop up.
  - [ ] Affected source code:
    - [Link 1](https://core.trac.wordpress.org/browser/tags/4.9/src/wp-includes/class-wp-xmlrpc-server.php#L5877)
4. (Optional) Vulnerability Name or ID
  - [ ] Summary: 
    - Vulnerability types:
    - Tested in version:
    - Fixed in version: 
  - [ ] GIF Walkthrough: 
  - [ ] Steps to recreate: 
  - [ ] Affected source code:
    - [Link 1](https://core.trac.wordpress.org/browser/tags/version/src/source_file.php)
5. (Optional) Vulnerability Name or ID
  - [ ] Summary: 
    - Vulnerability types:
    - Tested in version:
    - Fixed in version: 
  - [ ] GIF Walkthrough: 
  - [ ] Steps to recreate: 
  - [ ] Affected source code:
    - [Link 1](https://core.trac.wordpress.org/browser/tags/version/src/source_file.php) 

## Assets

List any additional assets, such as scripts or files

## Resources

- [WordPress Source Browser](https://core.trac.wordpress.org/browser/)
- [WordPress Developer Reference](https://developer.wordpress.org/reference/)

GIFs created with [LiceCap](http://www.cockos.com/licecap/).

## Notes

Describe any challenges encountered while doing the work

## License

    Copyright [2018] [Christopher Raley]

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

        http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
