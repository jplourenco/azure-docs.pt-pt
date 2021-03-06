A tabela seguinte mostra os tipos de gateways e o débito agregado estimado pelo SKU do gateway. Esta tabela aplica-se aos modelos de implementação clássica e Resource Manager. Há diferença de preços entre os SKUs de gateway. Para obter mais informações, veja [Preços do Gateway de VPN](https://azure.microsoft.com/pricing/details/vpn-gateway).

Tenha em atenção que o SKU do gateway UltraPerformance não está representado nesta tabela. Para obter informações sobre o SKU de UltraPerformance, consulte a documentação do [ExpressRoute](../articles/expressroute/expressroute-about-virtual-network-gateways.md).

|  | **Débito do Gateway de VPN (1)** | **Máximo de túneis IPsec do Gateway de VPN (2)** | **Débito do Gateway do ExpressRoute** | **Coexistência do ExpressRoute e do Gateway de VPN** |
| --- | --- | --- | --- | --- |
| **SKU Básico (3)(5)** |100 Mbps |10 |500 Mbps |Não |
| **SKU Padrão (4)(5)** |100 Mbps |10 |1000 Mbps |Sim |
| **SKU de Elevado Desempenho (4)** |200 Mbps |30 |2000 Mbps |Sim |

* (1) O débito da VPN é uma estimativa aproximada baseada em medidas entre VNets na mesma região do Azure. Não é um débito garantido para ligações entre locais na Internet. É a medida de débito mais alta possível.
* (2) O número de túneis refere-se às VPNs RouteBased. Uma VPN PolicyBased só pode suportar um túnel VPN de Rede de VPNs.
* (3) O BGP não é suportado para o SKU Básico.
* (4) As VPNs PolicyBased não são suportadas para este SKU. Só são suportadas para o SKU Básico.
* (5) As ligações do Gateway de VPN S2S no modo ativo/ativo não são suportadas por este SKU. O modo ativo/ativo é suportado apenas no SKU HighPerformance.



<!--HONumber=Jan17_HO1-->


