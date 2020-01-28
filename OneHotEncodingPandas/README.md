# Categorical Features One-Hot Encoding

There are different ways to encode categorical features:

## Pandas

### Get Dummies

`X = pd.get_dummies(X, prefix_sep="_", drop_first=True)`

`X.head()`

prefix_sep="_" generates new column name for new columns

drop_first=True drops the original categorical column after getting dummy to avoid multicollinearity

### Map

Pandas can also use map to implement LabelEncoder (examples see the jupyter)

## LabelEncoder

`from sklearn.preprocessing import LabelEncoder`

`le = LabelEncoder`

`X[categorical_cols] = X[categorical_cols].apply(lambda col: le.fit_transform(col))`

`X[categorical_cols].head(10)`

## OneHotEncoder

`from sklearn.preprocessing import OneHotEncoder`

`ohe = OneHotEncoder(categorical_features = categorical_feature_mask, sparse=False)`

`X_ohe = ohe.fit_transform(X)`



Reference:

1. https://towardsdatascience.com/encoding-categorical-features-21a2651a065c
2. https://zhuanlan.zhihu.com/p/78364889

