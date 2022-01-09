# Fuzzy-wuzzy

## Combining 2-3 fuzzy - wuzzy process for geeting good results

```
from fuzzywuzzy import fuzz
from fuzzywuzzy import process

def get_suggestion(value, value_list, n):
    if value not in value_list:
        result = process.extract(value, value_list, scorer=fuzz.partial_ratio)
        result = [i[0] for i in result[:n] if not pd.isna(i[0])]
        result = process.extract(
            value, value_list, scorer=fuzz.token_set_ratio)
        result = [i[0] for i in result[:n] if not pd.isna(i[0])]
        result = process.extract(value, result, scorer=fuzz.token_sort_ratio)

        return [i[0] for i in result if i[1]>=75]
    return [value]


match=get_suggestion(name, links, 1)
print(match)

```
