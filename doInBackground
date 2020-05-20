protected String doInBackground(String... strings) {
        HttpsURLConnection connection = null;
        HttpURLConnection connection2 = null;
        HttpURLConnection connection3 = null;
        BufferedReader reader = null;
        try{
            
            URL url = new URL(zeverURLlogin);
            connection = (HttpsURLConnection) url.openConnection();

            connection.setReadTimeout(7000);
            connection.setConnectTimeout(7000);
            connection.setRequestMethod("POST");
            connection.setDoInput(true);

            // Add any data you wish to post here
            byte[] outputInBytes = body.getBytes("UTF-8");
            OutputStream os = connection.getOutputStream();
            os.write( outputInBytes );
            os.close();

            //Finally connecting
            connection.connect();

            Log.d(TAG, "doInBackground: connection1: " + connection.getResponseCode());
            String newUrl = connection.getHeaderField("Location");
            Log.d(TAG, "doInBackground: redirection address " + newUrl);
            String cookies = connection.getHeaderField("Set-Cookie");
            Log.d(TAG, "doInBackground: cookies   " + cookies);
            String arr[] = cookies.split(";");
            Log.d(TAG, "doInBackground: cookie 0 " + arr[0]);

            Log.d(TAG, "doInBackground: cookie 1 " + arr[1]);

            Log.d(TAG, "doInBackground: cookie 2 " + arr[2]);
            connection.disconnect();
            
            URL newURL = new URL(connection.getHeaderField("Location"));

            connection2 = (HttpURLConnection) newURL.openConnection();
            connection2.setRequestMethod("GET");
            
            connection2.connect();

            Log.d(TAG, "doInBackground: connection2: " + connection2.getResponseCode());
            Log.d(TAG, "doInBackground: redirection address " + connection2.getHeaderField("Location"));
            Log.d(TAG, "doInBackground: cookies  " + connection2.getHeaderField("Set-Cookie"));

            URL newURL2 = new URL(connection2.getHeaderField("Location"));

            connection3 = (HttpURLConnection) newURL2.openConnection();
            connection3.setRequestMethod("GET");
            
            connection3.connect();

            Log.d(TAG, "doInBackground: connection3 address: " + newURL2);
            Log.d(TAG, "doInBackground: connection3: " + connection3.getResponseCode());
            Log.d(TAG, "doInBackground: redirection address " + connection3.getHeaderField("Location"));
            Log.d(TAG, "doInBackground: cookies  " + connection3.getHeaderField("Set-Cookie"));

            StringBuilder result = new StringBuilder();
            reader = new BufferedReader(new InputStreamReader(connection3.getInputStream()));
            String line;
            while(null != (line = reader.readLine())){
                result.append(line).append("\n");
            }
            mDownloadStatus = DownloadStatus.OK;
            Log.d(TAG, "doInBackground: result is" + result.toString());
            return result.toString();


        }
        }
