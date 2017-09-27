
## example 
fetch("http://localhost:1337/search",
	{
	method: 'POST', 
	body:JSON.stringify({
			body:{query: {match: {      url: {        query: 'about'      }    }  }},
			index:"general"
		})
	}).then(function(e){console.log(e)

	})

fetch("http://localhost:1337/search",
	{
	method: 'POST', 
	body:JSON.stringify({
			body:{query: {
				multi_match: {
				  query: 'about',
				  fields: ['url','author','title','userSynopsis']
				}  
			}},
			index:"general"
		})
	}).then(function(e){console.log(e)

	})


	q={searchTerms}&num={count?}&start={startIndex?}&lr={language?}&safe={safe?}&cx={cx?}&cref={cref?}&sort={sort?}&   filter={filter?}&gl={gl?}&cr={cr?}&googlehost={googleHost?}&c2coff={disableCnTwTranslation?}&    hq={hq?}&hl={hl?}&siteSearch={siteSearch?}&siteSearchFilter={siteSearchFilter?}&    exactTerms={exactTerms?}&excludeTerms={excludeTerms?}&linkSite={linkSite?}&    orTerms={orTerms?}&relatedSite={relatedSite?}&dateRestrict={dateRestrict?}&    lowRange={lowRange?}&highRange={highRange?}&searchType={searchType}&fileType={fileType?}&    rights={rights?}&imgSize={imgSize?}&imgType={imgType?}&imgColorType={imgColorType?}&    imgDominantColor={imgDominantColor?}&alt=json"  }