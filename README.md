# kmkk
Nombre del proyecto: erc-sdk-py yoel


Lenguaje: Python 3.9+

Dependencias:

- web3 para interactuar con la blockchain
- requests para realizar peticiones HTTP

Características:

- Soporte para ERC-20, ERC-721 y ERC-1155
- Métodos para obtener información de tokens, balances y transacciones
- Métodos para realizar transacciones y llamadas a contratos
- Soporte para redes de prueba y mainnet

LICENSE

Código:


import web3
from web3 import Web3

class ERC_API:
    def __init__(self, network: str = 'mainnet'):
        self.web3 = Web3(Web3.HTTPProvider(f'https://{network}.(link unavailable)'))

    def get_token_info(self, address: str):
        # Obtener información del token
        contract = self.web3.eth.contract(address=address, abi=ERC20_ABI)
        return contract.functions.name().call(), contract.functions.symbol().call()

    def get_balance(self, address: str, token_address: str):
        # Obtener balance de tokens
        contract = self.web3.eth.contract(address=token_address, abi=ERC20_ABI)
        return contract.functions.balanceOf(address).call()

    def send_transaction(self, from_address: str, to_address: str, amount: int, token_address: str):
        # Realizar transacción
        contract = self.web3.eth.contract(address=token_address, abi=ERC20_ABI)
        tx = contract.functions.transfer(to_address, amount).buildTransaction({
            'from': from_address,
            'gasPrice': self.web3.toWei('20', 'gwei'),
            'gas': 20000
        })
        return self.web3.eth.sendTransaction(tx)



from web3 import Web3

ERC20_ABI = [
    {
        'constant': True,
        'inputs': [{'name': '_owner', 'type': 'address'}],
        'name': 'balanceOf',
        'outputs': [{'name': '', 'type': 'uint256'}],
        'payable': False,
        'stateMutability': 'view',
        'type': 'function'
    },
    # ...
]

Instalación:

1. Clona el repositorio: `git clone 
2. Instala las dependencias: pip install -r requirements.txt
3. Importa el SDK en tu proyecto: from erc import ERC_API

Uso:


erc_api = ERC_API(network='mainnet')

# Obtener información del token
token_name, token_symbol = erc_api.get_token_info('0x...token_address...')

# Obtener balance de tokens
balance = erc_api.get_balance('0x...address...', '0x...token_address...')

# Realizar transacción
tx_hash = erc_api.send_transaction('0x...from_address...', '0x...to_address...', 100, '0x...token_address...')
