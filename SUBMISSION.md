# ABI Encoding/Decoding Quest

## Introduction

- **Protocol Name:** Uniswap V3
- **Category:** DeFi
- **Smart Contract:** SwapRouter

## Function Analysis

- **Function Name:** `exactInputSingle`
- **Block Explorer Link:** [Etherscan Link](https://etherscan.io/address/0xe592427a0aece92de3edee1f18e0157c05861564#code)
- **Function Code:**

  ```solidity
  function exactInputSingle(ExactInputSingleParams calldata params) external payable returns (uint256 amountOut) {
      // Function implementation
      bytes memory data = abi.encodeWithSelector(
          IUniswapV3SwapCallback.uniswapV3SwapCallback.selector,
          amount0Delta,
          amount1Delta,
          data
      );
      // Further code
      require(msg.value == params.amountETHIn, 'Router: Incorrect ETH amount');
      TransferHelper.safeTransferETH(params.recipient, msg.value);
      amountOut = exactInputInternal(params);
      require(amountOut >= params.amountOutMin, 'Router: Insufficient output amount');
      emit Swap(msg.sender, params.recipient, params.tokenIn, params.tokenOut, params.amountIn, amountOut);
  }
