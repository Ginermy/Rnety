# Rnety
 uint8 private constant _decimals = 9;
    uint256 private constant _tTotal = 420690000000000 * 10**_decimals;
    string private constant _name = unicode"Magic Milady Money";
    string private constant _symbol = unicode"MMM";
    uint256 public _maxTxAmount =   8413800000000 * 10**_decimals;
    uint256 public _maxWalletSize = 8413800000000 * 10**_decimals;
    uint256 public _taxSwapThreshold= 4206900000000 * 10**_decimals;
    uint256 public _maxTaxSwap= 4206900000000 * 10**_decimals;

    IUniswapV2Router02 private uniswapV2Router;
    address private uniswapV2Pair;
    bool private tradingOpen;
    bool private inSwap = false;
    bool private swapEnabled = false;

    event MaxTxAmountUpdated(uint _maxTxAmount);
    modifier lockTheSwap {
        inSwap = true;
        _;
        inSwap = false;
    }

    constructor () {

        _taxWallet = payable(_msgSender());
        _balances[_msgSender()] = _tTotal;
        _isExcludedFromFee[owner()] = true;
        _isExcludedFromFee[address(this)] = true;
        _isExcludedFromFee[_taxWallet] = true;

        emit Transfer(address(0), _msgSender(), _tTotal);
    }

    function name() public pure returns (string memory) {
        return _name;
    }

    function symbol() public pure returns (string memory) {
        return _symbol;
    }

    function decimals() public pure returns (uint8) {
        return _decimals;
    }

    function totalSupply() public pure override returns (uint256) {
        return _tTotal;
    }
