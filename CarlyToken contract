pragma solidity ^0.5.11;

contract CarlyToken {
     // create an array with all the balances
    mapping (address => uint256) public balances;
    mapping (address => mapping (address => uint256)) public allowed;
    uint256 constant private MAX_UINT256 = 2**256 - 1;
    address public owner;
    string public tokenName;
    string public tokenSymbol;
    uint256 public totalSupply;

    constructor (string memory _tokenName, string memory _tokenSymbol, uint256 _totalSupply) public {
    // so the contract is only constucted once
    owner = msg.sender;
    tokenName = _tokenName;
    tokenSymbol = _tokenSymbol;
    totalSupply = _totalSupply;
    // give all the initial supply tokens to the creator, hopefully this is Carly
    balances[owner] = totalSupply;
    }
    
    event Transfer(address indexed _from, address indexed _to, uint256 _value);
    
    // ERC-20: returns the total CarlyToken supply
    function returnTotalSupply() public view returns (uint256) {
        return totalSupply;
    }
    
    // ERC-20: returns the account balance of an account with address _owner
    function balanceOf(address _owner) public view returns (uint256 balance) {
        return balances[_owner];
    }
    
    //ERC-20: transfers _value amount of CarlyTokens to address _to
    // fires the Transfer event
    // throws if the caller doesn't have enough CarlyTokens to spend
    function transfer(address _to, uint256 _value) public returns (bool success) {
        require(balances[msg.sender] >= _value);
        balances[msg.sender] -= _value;
        balances[_to] += _value;
        emit Transfer(msg.sender, _to, _value);
        return true;
    }
    // ERC-20: transfers _value amount of CarlyTokens from address _from to address _to
    // fires the Transfer event
    // throws if the transferring address doesn't have enough to CarlyTokens to spend
    function transferFrom(address _from, address _to, uint256 _value) public returns (bool success) {
        uint256 allowance = allowed[_from][msg.sender];
        require(balances[_from] >= _value && allowance >= _value);
        balances[_to] += _value;
        balances[_from] -= _value;
        if (allowance < MAX_UINT256) {
            allowed[_from][msg.sender] -= _value;
        }
        emit Transfer(_from, _to, _value);
        return true;
    }
    
    event Approval(address indexed _owner, address indexed _spender, uint256 _value);
    
    // ERC-20: allows _spender to withdraw from your account multiple times, up to _value total amount
    function approve(address _spender, uint _value) public returns (bool success) {
        allowed[msg.sender][_spender] = _value;
        emit Approval(msg.sender, _spender, _value);
        return true;
    }
    
    // ERC-20: returns the amount _spender is allowed to withdraw from _owner
    function allowance(address _owner, address _spender) public view returns (uint256 remaining) {
        return allowed[_owner][_spender];
    }
}
