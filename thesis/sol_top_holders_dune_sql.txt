SELECT
  address,
  sol_balance,
  token_balance_owner AS wallet,
  NOW() AS current_block_time
FROM solana_utils.latest_balances
ORDER BY
  sol_balance DESC
LIMIT 1500

## @meitedaf/Solana top holders
