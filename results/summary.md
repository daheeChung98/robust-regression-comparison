# Summary

## Best predictive performance

| Model | RMSE | MAE | R<sup>2</sup> |
|------|------|------|------|
| OLS | 0.7456 | 0.5332 | 0.5758 |
| Ridge | 0.7456 | 0.5332 | 0.5758 |
| LASSO | 0.7404 | 0.5353 | 0.5816 |
| Huber | 0.7584 | 0.5158 | 0.5610 |

## Main observations

- Ridge behaved similarly to OLS.
- LASSO selected variables automatically.
- Huber changed coefficients considerably.

## Future work

Inject synthetic outliers (5%, 10%, 20%).
