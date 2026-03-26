# Medidas DAX Utilizadas en el Dashboard

## Medidas de Ventas Totales

```dax
Total Ventas = SUM('ps_sales_2025'[Total Sales])
Ventas NA = SUM('ps_sales_2025'[NA Sales])
Ventas PAL = SUM('ps_sales_2025'[PAL Sales])
Ventas Japon = SUM('ps_sales_2025'[Japan Sales])
Ventas Otras = SUM('ps_sales_2025'[Other Sales])

% Ventas NA = DIVIDE([Ventas NA], [Total Ventas], 0)
% Ventas PAL = DIVIDE([Ventas PAL], [Total Ventas], 0)
% Ventas Japon = DIVIDE([Ventas Japon], [Total Ventas], 0)
% Ventas Otras = DIVIDE([Ventas Otras], [Total Ventas], 0)

Promedio Ventas por Juego = AVERAGE('ps_sales_2025'[Total Sales])