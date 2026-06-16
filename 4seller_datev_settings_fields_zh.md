# 4Seller DATEV 收入导出设置字段说明

本文档用于说明 `4seller_datev_settings_page.html` 中每个系统设置字段的业务含义和开发规则。

## 1. Allgemeines 基础信息

| 字段 | 是否必填 | 输入方式 | 字段含义 | 开发注意点 |
|---|---:|---|---|---|
| DATEV Beraternummer | 是 | 数字，最多 7 位 | DATEV 文件头中的税务顾问编号。 | 由会计师或税务顾问提供，导入 DATEV 时需要匹配。导出前校验数字和长度。 |
| Mandantennummer | 是 | 数字，最多 5 位 | DATEV 中的客户/企业编号。 | 必须与会计师在 DATEV 中维护的客户主数据一致。 |
| Länge Sachkontennummern | 是 | 下拉：4-8 | 总账科目编号长度。 | 用于校验收入科目、债务人科目、支付过渡科目等账号长度。 |
| Export Format | 是 | 下拉 | 导出文件格式。 | 当前范围为 `DATEV Format (CSV)`，后续可扩展其他格式。 |
| Beginn des Wirtschaftsjahres Tag | 是 | 下拉 | 财年开始日。 | 与月份一起校验导出期间，避免跨财年混导。 |
| Monat | 是 | 下拉 | 财年开始月份。 | 与开始日一起判断会计年度。 |

## 2. Erlöskonten volle Umsatzsteuer 标准税率收入科目

| 字段 | 是否必填 | 输入方式 | 字段含义 | 开发注意点 |
|---|---:|---|---|---|
| Land | 是 | 国家规则/默认行 | 适用国家。 | `Alle anderen Länder` 表示没有国家专属规则时的默认规则。 |
| Konto | 是 | 数字科目，最多 8 位 | 标准税率销售收入科目。 | 例如 SKR03 常见科目 `8400`。长度需符合 `Länge Sachkontennummern`。 |
| + | 可选 | 操作按钮 | 新增国家专属规则。 | 同一分组内不要重复同一个国家。 |

## 3. Erlöskonten ermäßigte Umsatzsteuer 优惠税率收入科目

| 字段 | 是否必填 | 输入方式 | 字段含义 | 开发注意点 |
|---|---:|---|---|---|
| Land | 是 | 国家规则/默认行 | 优惠税率适用国家。 | `Alle anderen Länder` 为默认规则。 |
| Konto | 是 | 数字科目，最多 8 位 | 优惠税率销售收入科目。 | 当订单商品税率为优惠税率时使用。 |
| + | 可选 | 操作按钮 | 新增优惠税率国家规则。 | 避免重复国家。 |

## 4. Erlöskonten digitale Artikel 数字商品收入科目

| 字段 | 是否必填 | 输入方式 | 字段含义 | 开发注意点 |
|---|---:|---|---|---|
| Land | 是 | 国家规则/默认行 | 数字商品或电子服务适用国家。 | 数字商品通常可能涉及目的地国家税务逻辑。 |
| Konto | 是 | 数字科目，最多 8 位 | 数字商品收入科目。 | 按科目长度规则校验。 |
| Steuerschlüssel | 可选 | 数字，最多 3 位 | DATEV 税务键。 | 当税务处理不能仅通过科目判断，或会计要求明确税务键时填写。 |
| + | 可选 | 操作按钮 | 新增数字商品国家规则。 | 避免重复国家。 |

## 5. Erlöskonten für im Inland nicht steuerbare Umsätze 德国境内不征税销售收入科目

| 字段 | 是否必填 | 输入方式 | 字段含义 | 开发注意点 |
|---|---:|---|---|---|
| Land | 可选 | 国家规则/默认行 | 不在德国征税的销售适用国家。 | 该分组为可选，只有配置后才使用。 |
| Konto | 可选 | 数字科目，最多 8 位 | 德国境内不征税销售收入科目。 | 未配置时不应套用该类记账规则。 |
| Steuerschlüssel | 可选 | 数字，最多 3 位 | 该不征税场景的 DATEV 税务键。 | 由会计规则决定是否需要。 |
| + | 可选 | 操作按钮 | 新增国家规则。 | 避免重复国家。 |

## 6. Erlöskonten für im Inland nicht steuerbare Umsätze, ermäßigter Steuersatz 德国境内不征税销售优惠税率

| 字段 | 是否必填 | 输入方式 | 字段含义 | 开发注意点 |
|---|---:|---|---|---|
| Land | 可选 | 国家规则/默认行 | 不征税且商品本身属于优惠税率逻辑的国家规则。 | 该分组为可选。 |
| Konto | 可选 | 数字科目，最多 8 位 | 不征税优惠税率场景收入科目。 | 只有配置后才使用。 |
| Steuerschlüssel | 可选 | 数字，最多 3 位 | 不征税优惠税率场景的 DATEV 税务键。 | 由会计规则决定。 |
| + | 可选 | 操作按钮 | 新增国家规则。 | 避免重复国家。 |

## 7. Erlöskonten steuerfreie Umsätze Drittland 第三国免税销售收入科目

| 字段 | 是否必填 | 输入方式 | 字段含义 | 开发注意点 |
|---|---:|---|---|---|
| Land | 可选 | 国家规则/默认行 | 欧盟外第三国免税销售适用国家。 | 该分组为可选。 |
| Konto | 可选 | 数字科目，最多 8 位 | 第三国免税销售收入科目。 | 只有配置后才使用。 |
| + | 可选 | 操作按钮 | 新增第三国国家规则。 | 避免重复国家。 |

## 8. Erlöskonten OSS Fernverkäufe OSS 远程销售收入科目

| 字段 | 是否必填 | 输入方式 | 字段含义 | 开发注意点 |
|---|---:|---|---|---|
| Land | 可选 | 欧盟目的地国家 | OSS 远程销售的目的地国家。 | 与 OSS 申报逻辑相关。 |
| Konto | 可选 | 数字科目，最多 8 位 | OSS 标准税率销售收入科目。 | 当订单符合 OSS 且为标准税率时使用。 |
| Steuerschlüssel | 可选 | 数字，最多 3 位 | 目的地国家 VAT 处理对应的 DATEV 税务键。 | 由会计规则决定。 |
| + | 可选 | 操作按钮 | 新增 OSS 国家规则。 | 避免重复国家。 |

## 9. Erlöskonten OSS Fernverkäufe, ermäßigter Steuersatz OSS 远程销售优惠税率

| 字段 | 是否必填 | 输入方式 | 字段含义 | 开发注意点 |
|---|---:|---|---|---|
| Land | 可选 | 欧盟目的地国家 | OSS 优惠税率远程销售目的地国家。 | 该分组为可选。 |
| Konto | 可选 | 数字科目，最多 8 位 | OSS 优惠税率销售收入科目。 | 当订单符合 OSS 且为优惠税率时使用。 |
| Steuerschlüssel | 可选 | 数字，最多 3 位 | OSS 优惠税率对应 DATEV 税务键。 | 由会计规则决定。 |
| + | 可选 | 操作按钮 | 新增 OSS 优惠税率国家规则。 | 避免重复国家。 |

## 10. Sonstige Erlöskonten 其他收入科目

| 字段 | 是否必填 | 输入方式 | 字段含义 | 开发注意点 |
|---|---:|---|---|---|
| Erlöskonto Kleinunternehmer | 可选 | 数字科目，最多 8 位 | 小规模企业收入科目。 | 当企业按小规模规则处理、发票不显示 VAT 时使用。 |
| Erlöskonto keine Umsatzsteuer | 可选 | 数字科目，最多 8 位 | 无增值税收入兜底科目。 | 当订单不记 VAT 且没有更具体规则匹配时使用，避免导出报错。 |
| Erlöskonto steuerfreie innergemeinschaftliche Umsätze | 可选 | 数字科目，最多 8 位 | 欧盟内 B2B 免税销售收入科目。 | 需要税务逻辑识别 EU intra-community 免税销售。 |
| Erlöskonto Differenzbesteuerung | 可选 | 数字科目，最多 8 位 | 差额征税收入科目。 | 仅当订单被标记为差额征税时使用。 |

## 11. Debitorkonten 债务人科目

| 字段 | 是否必填 | 输入方式 | 字段含义 | 开发注意点 |
|---|---:|---|---|---|
| Modus | 是 | 下拉：Sammelkonto、Kundennummer | 控制债务人对方科目的生成方式。 | `Sammelkonto` 表示所有客户应收使用一个汇总科目；`Kundennummer` 表示按客户编号生成债务人科目。 |
| Debitoren Sammelkonto | 条件必填 | 数字科目，最多 8 位 | 当模式为 `Sammelkonto` 时使用的债务人汇总科目。 | `Modus = Sammelkonto` 时必填，通常作为收入科目的对方科目。 |

## 12. Sammelkonten pro Zahlart 按支付方式的过渡科目

| 字段 | 是否必填 | 输入方式 | 字段含义 | 开发注意点 |
|---|---:|---|---|---|
| Zahlart | 可选 | 下拉或文本 | 订单或支付交易中的支付方式。 | 示例：PayPal、Banküberweisung。 |
| Konto | 可选 | 数字科目，最多 8 位 | 该支付方式对应的过渡/清算科目。 | 当需要按支付方式区分收款过渡账户时使用。 |
| + | 可选 | 操作按钮 | 新增支付方式规则。 | 避免重复支付方式。 |

## 13. Sonstiges / Belegtexte 其他 / 凭证文本

| 字段 | 是否必填 | 输入方式 | 字段含义 | 开发注意点 |
|---|---:|---|---|---|
| Umsatzkontonummern pro Shop erhöhen | 可选 | 数字偏移量，最多 4 位 | 按店铺递增收入科目编号。 | 例如基础科目 `8400` 加偏移量 `2`，可用于区分不同店铺收入。具体规则需与会计确认。 |
| Debitorenkontonummern pro Shop erhöhen | 可选 | 数字偏移量，最多 4 位 | 按店铺递增债务人科目编号。 | 当债务人科目需要按店铺分开时使用。 |
| Eigenschaft Belegdatum | 是 | 下拉：Bestelldatum、Zahldatum、Rechnungsdatum、Versanddatum | 决定哪个订单日期导出为 DATEV `Belegdatum`。 | 会影响会计期间，需要与会计期望一致。 |
| Belegtext | 可选 | 普通文本模板 + 占位符 | DATEV 凭证文本列。 | 导出为一个文本值，由固定文本和占位符拼接而成。 |
| Belegfeld 1 | 可选 | 普通文本模板 + 占位符 | DATEV 凭证字段 1。 | 通常用于发票号、外部订单号或主要凭证引用。 |
| Belegfeld 2 | 可选 | 普通文本模板 + 占位符 | DATEV 凭证字段 2。 | 通常用于店铺名、发货日期或次要引用。 |

## 14. 占位符变量

| 占位符 | 含义 | 常见用途 |
|---|---|---|
| `{BuyerName}` | 买家姓名 | Belegtext |
| `{CustomerNumber}` | 客户编号 | 债务人或凭证引用 |
| `{InvoiceNumber}` | 发票号 | Belegfeld 1 |
| `{OrderDate}` | 订单日期 | Belegtext |
| `{OrderRef}` | 外部订单号 | Belegtext 或 Belegfeld 1 |
| `{PaymentTransactionId}` | 支付交易 ID | Belegtext 或审计追踪 |
| `{Platform}` | 销售平台 | Belegtext |
| `{ShipDate}` | 发货日期 | Belegfeld 2 |
| `{ShopName}` | 店铺名称 | Belegfeld 2 |
| `{TotalSum}` | 订单总金额 | 当需要在文本中显示金额时使用 |

## 15. 实现规则

- 必填字段在导出前必须校验。
- 可选科目分组只有配置了科目值后才参与导出。
- 科目输入长度应遵守 `Länge Sachkontennummern`。
- `Steuerschlüssel` 应为数字，最多 3 位。
- 国家专属规则优先级高于 `Alle anderen Länder`。
- 凭证字段保持普通文本模板；变量 chip 只是输入引导，不改变最终值的数据结构。
- DATEV/Billbee 的德文字段名建议在数据模型中保留，尤其是直接对应会计概念的字段。
