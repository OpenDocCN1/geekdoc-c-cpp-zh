```
```cpp
curl_easy_setopt(curl, CURLOPT_USERNAME, username.c_str());

curl_easy_setopt(curl, CURLOPT_PASSWORD, password.c_str());

curl_easy_setopt(curl, CURLOPT_POSTQUOTE, headerlist);

res = curl_easy_perform(curl);

if(res != CURLE_OK)
    fprintf(stderr, "curl_easy_perform() failed: %s\n",
            curl_easy_strerror(res));

curl_slist_free_all(headerlist);

curl_easy_cleanup(curl);

}

curl_global_cleanup();

return 0;

}
```
```