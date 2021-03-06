# blank

The following is an example of how one might display errors/warnings in the build where lodash.template is used due to the unresolved CVE.

```js
/*eslint no-restricted-imports: ["error", { paths: [{
    name: "lodash",
    importNames: ["template"],        
    message: "Importing 'lodash.template' from 'lodash' is not allowed due to an unresolved vuneralbility CVE-2021-23337 (https://nvd.nist.gov/vuln/detail/CVE-2021-23337)."
}]}]*/


// naughty imports
import * as _ from "lodash";
import { template as t} from "lodash";

_.template('', { variable: '){console.log(process.env)}; with(obj' })()
t('', { variable: '){console.log(process.env)}; with(obj' })()


// a permitted lodash imports
// last is imported as 'template' for demonstration: don't do this
import { first, last as template} from "lodash";
{
  let words = ['sky', 'wood', 'forest', 'falcon',
    'pear', 'ocean', 'universe'];
  let fel = first(words);
  let lel = template(words);
  console.log(fel);
  console.log(lel);
}
```

To see this in action, [Go Here](https://eslint.org/demo#eyJ0ZXh0IjoiLyplc2xpbnQgbm8tcmVzdHJpY3RlZC1pbXBvcnRzOiBbXCJlcnJvclwiLCB7IHBhdGhzOiBbe1xuICAgIG5hbWU6IFwibG9kYXNoXCIsXG4gICAgaW1wb3J0TmFtZXM6IFtcInRlbXBsYXRlXCJdLCAgICAgICAgXG4gICAgbWVzc2FnZTogXCJJbXBvcnRpbmcgJ2xvZGFzaC50ZW1wbGF0ZScgZnJvbSAnbG9kYXNoJyBpcyBub3QgYWxsb3dlZCBkdWUgdG8gYW4gdW5yZXNvbHZlZCB2dW5lcmFsYmlsaXR5IENWRS0yMDIxLTIzMzM3IChodHRwczovL252ZC5uaXN0Lmdvdi92dWxuL2RldGFpbC9DVkUtMjAyMS0yMzMzNykuXCJcbn1dfV0qL1xuXG5cbi8vIG5hdWdodHkgaW1wb3J0c1xuaW1wb3J0ICogYXMgXyBmcm9tIFwibG9kYXNoXCI7XG5pbXBvcnQgeyB0ZW1wbGF0ZSBhcyB0fSBmcm9tIFwibG9kYXNoXCI7XG5cbl8udGVtcGxhdGUoJycsIHsgdmFyaWFibGU6ICcpe2NvbnNvbGUubG9nKHByb2Nlc3MuZW52KX07IHdpdGgob2JqJyB9KSgpXG50KCcnLCB7IHZhcmlhYmxlOiAnKXtjb25zb2xlLmxvZyhwcm9jZXNzLmVudil9OyB3aXRoKG9iaicgfSkoKVxuXG5cbi8vIGEgcGVybWl0dGVkIGxvZGFzaCBpbXBvcnRzXG4vLyBsYXN0IGlzIGltcG9ydGVkIGFzICd0ZW1wbGF0ZScgZm9yIGRlbW9uc3RyYXRpb246IGRvbid0IGRvIHRoaXNcbmltcG9ydCB7IGZpcnN0LCBsYXN0IGFzIHRlbXBsYXRlfSBmcm9tIFwibG9kYXNoXCI7XG57XG4gIGxldCB3b3JkcyA9IFsnc2t5JywgJ3dvb2QnLCAnZm9yZXN0JywgJ2ZhbGNvbicsXG4gICAgJ3BlYXInLCAnb2NlYW4nLCAndW5pdmVyc2UnXTtcbiAgbGV0IGZlbCA9IGZpcnN0KHdvcmRzKTtcbiAgbGV0IGxlbCA9IHRlbXBsYXRlKHdvcmRzKTtcbiAgY29uc29sZS5sb2coZmVsKTtcbiAgY29uc29sZS5sb2cobGVsKTtcbn1cbiIsIm9wdGlvbnMiOnsicGFyc2VyT3B0aW9ucyI6eyJlY21hVmVyc2lvbiI6ImxhdGVzdCIsInNvdXJjZVR5cGUiOiJtb2R1bGUiLCJlY21hRmVhdHVyZXMiOnt9fSwicnVsZXMiOnsiY29uc3RydWN0b3Itc3VwZXIiOjIsImZvci1kaXJlY3Rpb24iOjIsImdldHRlci1yZXR1cm4iOjIsIm5vLWFzeW5jLXByb21pc2UtZXhlY3V0b3IiOjIsIm5vLWNhc2UtZGVjbGFyYXRpb25zIjoyLCJuby1jbGFzcy1hc3NpZ24iOjIsIm5vLWNvbXBhcmUtbmVnLXplcm8iOjIsIm5vLWNvbmQtYXNzaWduIjoyLCJuby1jb25zdC1hc3NpZ24iOjIsIm5vLWNvbnN0YW50LWNvbmRpdGlvbiI6Miwibm8tY29udHJvbC1yZWdleCI6Miwibm8tZGVidWdnZXIiOjIsIm5vLWRlbGV0ZS12YXIiOjIsIm5vLWR1cGUtYXJncyI6Miwibm8tZHVwZS1jbGFzcy1tZW1iZXJzIjoyLCJuby1kdXBlLWVsc2UtaWYiOjIsIm5vLWR1cGUta2V5cyI6Miwibm8tZHVwbGljYXRlLWNhc2UiOjIsIm5vLWVtcHR5IjoyLCJuby1lbXB0eS1jaGFyYWN0ZXItY2xhc3MiOjIsIm5vLWVtcHR5LXBhdHRlcm4iOjIsIm5vLWV4LWFzc2lnbiI6Miwibm8tZXh0cmEtYm9vbGVhbi1jYXN0IjoyLCJuby1leHRyYS1zZW1pIjoyLCJuby1mYWxsdGhyb3VnaCI6Miwibm8tZnVuYy1hc3NpZ24iOjIsIm5vLWdsb2JhbC1hc3NpZ24iOjIsIm5vLWltcG9ydC1hc3NpZ24iOjIsIm5vLWlubmVyLWRlY2xhcmF0aW9ucyI6Miwibm8taW52YWxpZC1yZWdleHAiOjIsIm5vLWlycmVndWxhci13aGl0ZXNwYWNlIjoyLCJuby1sb3NzLW9mLXByZWNpc2lvbiI6Miwibm8tbWlzbGVhZGluZy1jaGFyYWN0ZXItY2xhc3MiOjIsIm5vLW1peGVkLXNwYWNlcy1hbmQtdGFicyI6Miwibm8tbmV3LXN5bWJvbCI6Miwibm8tbm9ub2N0YWwtZGVjaW1hbC1lc2NhcGUiOjIsIm5vLW9iai1jYWxscyI6Miwibm8tb2N0YWwiOjIsIm5vLXByb3RvdHlwZS1idWlsdGlucyI6Miwibm8tcmVkZWNsYXJlIjoyLCJuby1yZWdleC1zcGFjZXMiOjIsIm5vLXNlbGYtYXNzaWduIjoyLCJuby1zZXR0ZXItcmV0dXJuIjoyLCJuby1zaGFkb3ctcmVzdHJpY3RlZC1uYW1lcyI6Miwibm8tc3BhcnNlLWFycmF5cyI6Miwibm8tdGhpcy1iZWZvcmUtc3VwZXIiOjIsIm5vLXVuZGVmIjoyLCJuby11bmV4cGVjdGVkLW11bHRpbGluZSI6Miwibm8tdW5yZWFjaGFibGUiOjIsIm5vLXVuc2FmZS1maW5hbGx5IjoyLCJuby11bnNhZmUtbmVnYXRpb24iOjIsIm5vLXVuc2FmZS1vcHRpb25hbC1jaGFpbmluZyI6Miwibm8tdW51c2VkLWxhYmVscyI6Miwibm8tdW51c2VkLXZhcnMiOjIsIm5vLXVzZWxlc3MtYmFja3JlZmVyZW5jZSI6Miwibm8tdXNlbGVzcy1jYXRjaCI6Miwibm8tdXNlbGVzcy1lc2NhcGUiOjIsIm5vLXdpdGgiOjIsInJlcXVpcmUteWllbGQiOjIsInVzZS1pc25hbiI6MiwidmFsaWQtdHlwZW9mIjoyLCJuby1yZXN0cmljdGVkLWltcG9ydHMiOjJ9LCJlbnYiOnsiYnJvd3NlciI6ZmFsc2UsIm5vZGUiOnRydWV9fX0=)
