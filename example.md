```rust
pub fn merge(
    iter: impl Iterator<Item = TokenId>,
    merge_if: impl Fn(TokenId, TokenId) -> Option<TokenId>,
) -> Vec<TokenId> {
    let mut result = vec![];

    let mut pairs = iter.pairs();
    while let Some((id0, id1)) = pairs.next() {
        if let Some(merged) = merge_if(id0, id1) {
            result.push(merged);
            pairs.next();
        } else {
            result.push(id0);
        }
    }

    if let Some(id) = pairs.final_item() {
        result.push(id);
    }

    result
}
```
