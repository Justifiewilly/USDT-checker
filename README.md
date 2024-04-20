from web3 import Web3

# Connect to an Ethereum node
web3 = Web3(Web3.HTTPProvider('https://mainnet.infura.io/v3/YOUR_INFURA_PROJECT_ID'))

# USDT contract address and ABI (Application Binary Interface)
usdt_contract_address = '0xdAC17F958D2ee523a2206206994597C13D831ec7'
usdt_contract_abi = [
    {
        "constant": True,
        "inputs": [{"name": "_owner", "type": "address"}],
        "name": "balanceOf",
        "outputs": [{"name": "balance", "type": "uint256"}],
        "type": "function"
    }
]

# Wallet address to check
wallet_address = '0xYourWalletAddressHere'

# Instantiate contract
usdt_contract = web3.eth.contract(address=usdt_contract_address, abi=usdt_contract_abi)

# Get USDT balance
usdt_balance = usdt_contract.functions.balanceOf(wallet_address).call()

# Convert balance from Wei to USDT (USDT has 6 decimal places)
usdt_balance_in_usdt = usdt_balance / 10**6

print(f'USDT balance in wallet {wallet_address}: {usdt_balance_in_usdt} USDT')
