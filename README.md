# webView
android

this is used to take runtime permission


 //for video recording
            // Grant permissions for camera
            @RequiresApi(api = Build.VERSION_CODES.LOLLIPOP)
            @Override
            public void onPermissionRequest(final PermissionRequest request) {

                if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.M) {
                    int hasCameraPermission = checkSelfPermission(Manifest.permission.CAMERA);
                    Log.d(TAG, "has camera permission: " + hasCameraPermission);
                    int hasRecordPermission = checkSelfPermission(Manifest.permission.RECORD_AUDIO);
                    Log.d(TAG, "has record permission: " + hasRecordPermission);
                    int hasAudioPermission = checkSelfPermission(Manifest.permission.MODIFY_AUDIO_SETTINGS);
                    Log.d(TAG, "has audio permission: " + hasAudioPermission);
                    List<String> permissions = new ArrayList<>();
                    if (hasCameraPermission != PackageManager.PERMISSION_GRANTED) {
                        permissions.add(Manifest.permission.CAMERA);
                    }
                    if (hasRecordPermission != PackageManager.PERMISSION_GRANTED) {
                        permissions.add(Manifest.permission.RECORD_AUDIO);
                    }
                    if (hasAudioPermission != PackageManager.PERMISSION_GRANTED) {
                        permissions.add(Manifest.permission.MODIFY_AUDIO_SETTINGS);
                    }

                    if (!permissions.isEmpty()) {
                        requestPermissions(permissions.toArray(new String[permissions.size()]),111);

                    }
                    Log.i(TAG, "onPermissionRequest");
                }

                MainActivity.this.runOnUiThread(new Runnable() {
                    @Override
                    public void run() {
                        request.grant(request.getResources());
                    }
                });
                if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.M) {
                    mPermissionRequest = request;
                }


            }



            @Override
            public void onPermissionRequestCanceled(PermissionRequest request) {
                super.onPermissionRequestCanceled(request);
                Toast.makeText(MainActivity.this, "Permission Denied", Toast.LENGTH_SHORT).show();
            }




manifest permission


<uses-permission android:name="android.permission.CAMERA"/>
<uses-permission android:name="android.permission.RECORD_AUDIO" />
<uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS" />
<uses-feature android:name="android.hardware.camera"
        android:required="true" />
