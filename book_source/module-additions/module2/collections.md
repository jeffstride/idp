# Collections

This is a Cheatsheet of sorts to summarize Python's collection classes.

## Summary
|Action|List|Tuple|Set|Dictionary|
|------|----|-----|---|----------|
|Create|a = [ ]</br>a = list()|t = ( , )</br>t = tuple()|s = set( )|d = { }</br>d = dict( )|
|initialize|a = [ 1, 2 ]|t = (1, 2)|s = { 1, 2 }|d = { 'a': 1 }|
|add</br>insert|a.append(obj)</br>a.insert(idx, obj)|t = t + ( obj, )|s.add(3)|d['b'] = 2|
|contains?|if obj in a|if obj in t|if obj in s|if 'key' in d|
|remove|a.remove(obj)</br>a.pop(index)</br>a.pop()|N/A|s.remove(obj)</br>s.pop()|d.pop(key)</br>d.pop(key, def_val)</br>del d[key]</br>d.popitem()|
|get</br>set|v = a[index]|v = t[index]</br>i1,i2 = t|N/A|v = d['a']</br>v = d.get('a', v)|



