1o

run_query =
fn query_def ->
Process.sleep(2000)
"#{query_def} result"
end

2o

run_query.("query 01")

3o

Enum.map(
  1..5,
  fn index ->
    query_def = "query 0#{index}"
    run_query.(query_def) end
)

4o

spawn(fn ->
  query_result = run_query.("query 01")
  IO.puts(query_result)
  end
)

5o

async_query =
fn query_def ->
  spawn(fn ->
    query_result = run_query.(query_def)
    IO.puts(query_result)
    end
  )
end

6o

async_query.("query 01")

7o

Enum.each(1..5, &async_query.("query 0#{&1}"))
