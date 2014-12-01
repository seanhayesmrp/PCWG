# Power Curve Working Group collaborative</h1>
[PCWG Website](http://www.pcwg.org)


### Filtering:
To apply filters to your data a simple filter node can be added to the configuration xml.

To filter timestamps when the shear exponent is above 0.2:
```xml
<ns1:Filter>
			<ns1:DataColumn>Shear Exponent</ns1:DataColumn>
			<ns1:FilterType>Above</ns1:FilterType>
			<ns1:Inclusive>0</ns1:Inclusive>
			<ns1:FilterValue>0.2</ns1:FilterValue>
			<ns1:Active>1</ns1:Active>
</ns1:Filter>
```

A filter can be applied that is a function of another data column.
The derivation is calculated in the form (A*COLUMN +B)^C
A, B and C are optional and default to 1,0 and 1 respectively.

For example, to apply the filter [Turbulence] > “WS_stddev/(0.75*WSmean+5.6)”:
```xml
<ns1:Filter>
	<!-- IEC Turbulence Intensity Filter -->
	<ns1:FilterType>Above</ns1:FilterType>
	<ns1:DataColumn>Hub Turbulence</ns1:DataColumn>
	<ns1:Inclusive>0</ns1:Inclusive>
	<ns1:Active>1</ns1:Active>			
	<ns1:FilterValue>
		<ns1:ColumnFactor>
			<ns1:ColumnName>Mast1_60m_StdDeviation</ns1:ColumnName>
			<ns1:A>1</ns1:A><ns1:B>0</ns1:B><ns1:C>-1</ns1:C>
		</ns1:ColumnFactor>	
		<ns1:ColumnFactor>
			<ns1:ColumnName>Mast1_60m_WindSpeed</ns1:ColumnName>
			<ns1:A>0.75</ns1:A><ns1:B>5.6</ns1:B><ns1:C>1</ns1:C>
		</ns1:ColumnFactor>	
	</ns1:FilterValue>	
</ns1:Filter>
```

For example, to apply the filter [Turbulence] > “WS_stddev/(0.75*WSmean+5.6)”:
```xml
<ns1:Filter>
	<!-- IEC Turbulence Intensity Filter -->
	<ns1:FilterType>Above</ns1:FilterType>
	<ns1:DataColumn>Hub Turbulence</ns1:DataColumn>
	<ns1:Inclusive>0</ns1:Inclusive>
	<ns1:Active>1</ns1:Active>			
	<ns1:FilterValue>
		<ns1:ColumnFactor>
			<ns1:ColumnName>Mast1_60m_StdDeviation</ns1:ColumnName>
			<ns1:A>1</ns1:A><ns1:C>1</ns1:C>
		</ns1:ColumnFactor>	
		<ns1:ColumnFactor>
			<ns1:ColumnName>Mast1_60m_WindSpeed</ns1:ColumnName>
			<ns1:A>0.75</ns1:A><ns1:B>5.6</ns1:B><ns1:C>-1</ns1:C>
		</ns1:ColumnFactor>	
	</ns1:FilterValue>	
</ns1:Filter>
```

Finally, data can be excluded using OR and AND relationships.
For example, to filter timestamps when [Power] < 0 AND 14.5 < [Wind speed] <= 20 :

```xml
<ns1:Filter>			
	<ns1:Active>1</ns1:Active>
	<ns1:Relationship>
		<ns1:Conjunction>AND</ns1:Conjunction>
		<ns1:Clause>
			<ns1:DataColumn>Actual Power</ns1:DataColumn>
			<ns1:FilterType>Below</ns1:FilterType>
			<ns1:Inclusive>0</ns1:Inclusive>
			<ns1:FilterValue>0</ns1:FilterValue>					
		</ns1:Clause>
		<ns1:Clause>
			<ns1:DataColumn>Hub Wind Speed</ns1:DataColumn>
			<ns1:FilterType>Between</ns1:FilterType>
			<ns1:Inclusive>0</ns1:Inclusive>
			<ns1:FilterValue>14.5,20.000001</ns1:FilterValue>					
		</ns1:Clause>	
	</ns1:Relationship>
</ns1:Filter>
```		
