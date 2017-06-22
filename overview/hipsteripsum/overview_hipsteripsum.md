





<div class="notebook" id="staticInteractiveoverview_hipsteripsum">

  <div class="notebook__static-tutorial" data-tutorial="overview_hipsteripsum" data-is-quick-setup="true" data-link="https://mmitoraj.github.io/build/embedded.html#overview_hipsteripsum">
   
   
   <h3 id="get-access-token">Get access token</h3>
<p>To perform any operations with specific service, you always need an access token. For this purpose create an API Client for oAuth2 service.</p>
<pre><code class="lang-javascript">API.createClient(&#39;oAuth2Service&#39;,
&#39;https://devportal.yaas.io/services/oauth2/b1/api.raml&#39;);
</code></pre>
<p>Now get the token:</p>
<pre><code class="lang-javascript">AccessToken = oAuth2Service.token.post({
  &#39;client_id&#39; : &#39;en7kp4cbjgA2TuuihU3MxCEShMx5xaEF&#39;,
  &#39;client_secret&#39;:&#39;63gNfrpSnQWKQXEO&#39;,
  &#39;grant_type&#39; : &#39;client_credentials&#39;,
    &#39;token_type&#39;: &#39;Bearer&#39;,
  &#39;scope&#39;: &#39;hybris.tenant hybris.document_manage hybris.document_view&#39;
});
</code></pre>
<p>To make calls simpler and code cleaner, assign Id of returned object to a variable.</p>
<pre><code class="lang-javascript">access_token = AccessToken.body.access_token;
</code></pre>
<h3 id="create-api-client-for-document-service">Create API client for Document service</h3>
<pre><code class="lang-javascript">API.createClient(&#39;documentService&#39;,
&#39;https://devportal.yaas.io/services/document/b2/api.raml&#39;);
</code></pre>
<h3 id="create-a-simple-object">Create a simple object</h3>
<pre><code class="lang-javascript">comic_obj = documentService.tenant(&#39;itutorials&#39;).client(&#39;hybris.itutorials&#39;).data.type(&#39;comic&#39;).post({
&#39;kind&#39;: &#39;History&#39;,
&#39;name&#39;: &#39;Thorgal&#39;
}, {
  headers: {
    &#39;Authorization&#39;: &#39;Bearer &#39; + access_token,
    &#39;Content-type&#39; : &#39;application/json&#39;
           }
        }
  )
</code></pre>
<p>To make calls simpler and code cleaner, assign Id of returned object to a variable.</p>
<pre><code class="lang-javascript">id = comic_obj.body.id;
</code></pre>
<h3 id="retrieve-object-created-with-the-previous-step">Retrieve object created with the previous step</h3>
<pre><code class="lang-javascript">documentService.tenant(&#39;itutorials&#39;).client(&#39;hybris.itutorials&#39;).data.type(&#39;comic&#39;).dataId(id).get(null, {
  headers: {
    &#39;Authorization&#39;: &#39;Bearer &#39; + access_token,
    &#39;Content-type&#39; : &#39;application/json&#39;
           }
        }
  )
</code></pre>
<h3 id="update-an-object-with-additional-information">Update an object with additional information</h3>
<p>Perform a partial update on the object:</p>
<pre><code class="lang-javascript">documentService.tenant(&#39;itutorials&#39;).client(&#39;hybris.itutorials&#39;).data.type(&#39;comic&#39;).dataId(id).put({
 &#39;title&#39;: &#39;Child of the Stars&#39;
}, {
  headers: {
    &#39;Authorization&#39;: &#39;Bearer &#39; + access_token,
    &#39;Content-type&#39; : &#39;application/json&#39;
  },
  query: {
      &#39;partial&#39; : true
  }
})
</code></pre>
<h3 id="retrieve-the-same-object-to-ensure-that-proper-information-is-updated">Retrieve the same object to ensure that proper information is updated</h3>
<p>Get the object to make sure that it was updated. You can be sure it was as the <strong>modifiedAt</strong> date is also updated.</p>
<pre><code class="lang-javascript">documentService.tenant(&#39;itutorials&#39;).client(&#39;hybris.itutorials&#39;).data.type(&#39;comic&#39;).dataId(id).get(null, {
  headers: {
    &#39;Authorization&#39;: &#39;Bearer &#39; + access_token,
    &#39;Content-type&#39; : &#39;application/json&#39;
           }
        }
  )
</code></pre>
<h3 id="update-entire-object-with-new-information">Update entire object with new information</h3>
<p>Now perform full update of the object:</p>
<pre><code class="lang-javascript">documentService.tenant(&#39;itutorials&#39;).client(&#39;hybris.itutorials&#39;).data.type(&#39;comic&#39;).dataId(id).put({
  &#39;name&#39;: &#39;Thorgal&#39;,
  &#39;title&#39;: &#39;The Brand of the Exiles&#39;,
  &#39;kind&#39;: &#39;History&#39;
}, {
  headers: {
    &#39;Authorization&#39;: &#39;Bearer &#39; + access_token,
    &#39;Content-type&#39; : &#39;application/json&#39;
  }
})
</code></pre>
<h3 id="retrieve-the-same-object-to-ensure-proper-information-is-replaced">Retrieve the same object to ensure proper information is replaced</h3>
<pre><code class="lang-javascript">documentService.tenant(&#39;itutorials&#39;).client(&#39;hybris.itutorials&#39;).data.type(&#39;comic&#39;).dataId(id).get(null, {
  headers: {
    &#39;Authorization&#39;: &#39;Bearer &#39; + access_token,
    &#39;Content-type&#39; : &#39;application/json&#39;
           }
        }
  )
</code></pre>
<h3 id="remove-a-single-attribute-from-an-object">Remove a single attribute from an object</h3>
<pre><code class="lang-javascript">documentService.tenant(&#39;itutorials&#39;).client(&#39;hybris.itutorials&#39;).data.type(&#39;comic&#39;).dataId(id).attributeName(&#39;name&#39;).delete(null, {
    headers: {
   &#39;Authorization&#39;: &#39;Bearer &#39; + access_token,
  }
})
</code></pre>
<h3 id="remove-an-entire-object">Remove an Entire Object</h3>
<pre><code class="lang-javascript">documentService.tenant(&#39;itutorials&#39;).client(&#39;hybris.itutorials&#39;).data.type(&#39;comic&#39;).dataId(id).delete(null, {
    headers: {
   &#39;Authorization&#39;: &#39;Bearer &#39; + access_token,
  }
})
</code></pre>
<h3 id="retrieve-a-deleted-object-to-ensure-it-is-really-deleted">Retrieve a deleted object to ensure it is really deleted</h3>
<pre><code class="lang-javascript">documentService.tenant(&#39;itutorials&#39;).client(&#39;hybris.itutorials&#39;).data.type(&#39;comic&#39;).dataId(id).get(null, {
  headers: {
    &#39;Authorization&#39;: &#39;Bearer &#39; + access_token,
    &#39;Content-type&#39; : &#39;application/json&#39;
           }
        }
  )
</code></pre>
<h3 id="create-a-simple-object-with-the-custom-id">Create a simple object with the custom ID</h3>
<pre><code class="lang-javascript">documentService.tenant(&#39;itutorials&#39;).client(&#39;hybris.itutorials&#39;).data.type(&#39;comic&#39;).dataId(&#39;sampleId&#39;).post({
&quot;kind&quot;: &quot;History&quot;,
&quot;name&quot;: &quot;Thorgal&quot;
}, {
  headers: {
    &#39;Authorization&#39;: &#39;Bearer &#39; + AccessToken.body.access_token,
    &#39;Content-type&#39; : &#39;application/json&#39;
           }
        }
  )
</code></pre>
<pre><code class="lang-javascript">documentService.tenant(&#39;itutorials&#39;).client(&#39;hybris.itutorials&#39;).data.type(&#39;comic&#39;).dataId(&#39;sampleId&#39;).delete(null, {
    headers: {
   &#39;Authorization&#39;: &#39;Bearer &#39; + access_token,
  }
})
</code></pre>

  </div>

  <div id="notebookoverview_hipsteripsum">
    <iframe style="min-height: 430px;" class="notebook__interactive-tutorial u-transition-all width-100 interactive-tutorial" src="" scrolling="no" frameBorder="0" id="overview_hipsteripsum"></iframe>
  </div>

  <div class="notebook__loader">

  </div>

</div> <!-- ---
---
id: overview_hipsteripsum
title: 'Perform Simple CRUD Operations'
type: 'Tutorial'
service: 'Document'
interactive: true
order: 40
---

### Get access token

To perform any operations with specific service, you always need an access token. For this purpose create an API Client for oAuth2 service.

```javascript
API.createClient('oAuth2Service',
'https://devportal.yaas.io/services/oauth2/b1/api.raml');
```

Now get the token:

```javascript
AccessToken = oAuth2Service.token.post({
  'client_id' : 'en7kp4cbjgA2TuuihU3MxCEShMx5xaEF',
  'client_secret':'63gNfrpSnQWKQXEO',
  'grant_type' : 'client_credentials',
    'token_type': 'Bearer',
  'scope': 'hybris.tenant hybris.document_manage hybris.document_view'
});
```

To make calls simpler and code cleaner, assign Id of returned object to a variable.

```javascript
access_token = AccessToken.body.access_token;
```

### Create API client for Document service


```javascript
API.createClient('documentService',
'https://devportal.yaas.io/services/document/b2/api.raml');
```

### Create a simple object


```javascript
comic_obj = documentService.tenant('itutorials').client('hybris.itutorials').data.type('comic').post({
'kind': 'History',
'name': 'Thorgal'
}, {
  headers: {
    'Authorization': 'Bearer ' + access_token,
    'Content-type' : 'application/json'
           }
		}
  )
```

To make calls simpler and code cleaner, assign Id of returned object to a variable.


```javascript
id = comic_obj.body.id;
```

### Retrieve object created with the previous step


```javascript
documentService.tenant('itutorials').client('hybris.itutorials').data.type('comic').dataId(id).get(null, {
  headers: {
    'Authorization': 'Bearer ' + access_token,
    'Content-type' : 'application/json'
           }
		}
  )
```

### Update an object with additional information

Perform a partial update on the object:

```javascript
documentService.tenant('itutorials').client('hybris.itutorials').data.type('comic').dataId(id).put({
 'title': 'Child of the Stars'
}, {
  headers: {
    'Authorization': 'Bearer ' + access_token,
    'Content-type' : 'application/json'
  },
  query: {
  	'partial' : true
  }
})
```

### Retrieve the same object to ensure that proper information is updated


Get the object to make sure that it was updated. You can be sure it was as the **modifiedAt** date is also updated.


```javascript
documentService.tenant('itutorials').client('hybris.itutorials').data.type('comic').dataId(id).get(null, {
  headers: {
    'Authorization': 'Bearer ' + access_token,
    'Content-type' : 'application/json'
           }
		}
  )
```

### Update entire object with new information

Now perform full update of the object:

```javascript
documentService.tenant('itutorials').client('hybris.itutorials').data.type('comic').dataId(id).put({
  'name': 'Thorgal',
  'title': 'The Brand of the Exiles',
  'kind': 'History'
}, {
  headers: {
    'Authorization': 'Bearer ' + access_token,
    'Content-type' : 'application/json'
  }
})
```

### Retrieve the same object to ensure proper information is replaced


```javascript
documentService.tenant('itutorials').client('hybris.itutorials').data.type('comic').dataId(id).get(null, {
  headers: {
    'Authorization': 'Bearer ' + access_token,
    'Content-type' : 'application/json'
           }
		}
  )
```

### Remove a single attribute from an object


```javascript
documentService.tenant('itutorials').client('hybris.itutorials').data.type('comic').dataId(id).attributeName('name').delete(null, {
	headers: {
   'Authorization': 'Bearer ' + access_token,
  }
})
```

### Remove an Entire Object


```javascript
documentService.tenant('itutorials').client('hybris.itutorials').data.type('comic').dataId(id).delete(null, {
	headers: {
   'Authorization': 'Bearer ' + access_token,
  }
})
```

### Retrieve a deleted object to ensure it is really deleted


```javascript
documentService.tenant('itutorials').client('hybris.itutorials').data.type('comic').dataId(id).get(null, {
  headers: {
    'Authorization': 'Bearer ' + access_token,
    'Content-type' : 'application/json'
           }
		}
  )
```

### Create a simple object with the custom ID



```javascript
documentService.tenant('itutorials').client('hybris.itutorials').data.type('comic').dataId('sampleId').post({
"kind": "History",
"name": "Thorgal"
}, {
  headers: {
    'Authorization': 'Bearer ' + AccessToken.body.access_token,
    'Content-type' : 'application/json'
           }
		}
  )
```

```javascript
documentService.tenant('itutorials').client('hybris.itutorials').data.type('comic').dataId('sampleId').delete(null, {
	headers: {
   'Authorization': 'Bearer ' + access_token,
  }
})
```
 -->