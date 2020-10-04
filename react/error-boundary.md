# Error Boundary

## componentDidCatch vs getDerivedStateFromError

I find interesting that you can now use method **getDerivedStateFromError** instead of **componentDidCatch**, but _what is the difference? (except syntax)_

Actually you can use them both (see an example in [docs](https://reactjs.org/docs/react-component.html#componentdidcatch))

The difference is (from official documentation):

> getDerivedStateFromError() is called during the “render” phase, so side-effects are not permitted. For those use cases, use componentDidCatch() instead.

## re-mount ErrorBoundary by key prop (and why this is not good idea)

If you are using **ErrorBoundary** component and you catch some error on UI you have two options how to "clear" this error and back to UI that is hiding under the ErrorBoundary message:

- clear state of error inside ErrorBoundary (for example by clicking on button and call setState)
- use a "key" prop of ErrorBoundary with dynamic value

For example, it could be the value of the input. If you wrote some wrong value in input and catch the error (and ErrorBoundary hides your result block for example) you can re-mount (i.e. "clear" state of error in ErrorBoundary) by rewriting this value.

See the example below:

```ts
function App() {
  const [val, setVal] = React.useState("");

  function handleSubmit(newVal: string) {
    setVal(newVal);
  }

  return (
    <div>
      <Form val={val} onSubmit={handleSubmit} />
      <div>
        <ErrorBoundary
          FallbackComponent={ErrorBoundaryFallback}
          key={val} // re-mount this component every time when 'val' is changed
        >
          <ResultPanel val={val} />
        </ErrorBoundary>
      </div>
    </div>
  );
}
```

Also you can use this feature with component **ErrorBoundary** from module [react-error-boundary](https://github.com/bvaughn/react-error-boundary) and special prop **resetKeys** which is quite similar as **key** that we use

```ts
<ErrorBoundary FallbackComponent={ErrorBoundaryFallback} resetKeys={[val]}>
  {explode ? <ResultPanel /> : null}
</ErrorBoundary>
```

> 🚨 Unfortunately, this method is not good for performance. Every time when **val** is changed and **ErrorBoundary** is re-mount - inner component (in our case - **ResultPanel**) is re-mount too!

So how avoid this problem? You have two options:

- Just use the first option of how to clear error state (add a button with the handler which set the state of the error to null)

## Using FallbackComponent prop

Sometimes we need to display different error messages for different types of errors (for example runtime errors and server errors). We can add a prop called "FallbackComponent" to our own **ErrorBoundary** component and put different view-components into this prop based on the place where we're using our ErrorBoundary.

Example:

```ts
interface ErrorBoundaryState {
  error: Error | null;
}

interface FallbackProps {
  error: Error;
}

class ErrorBoundary extends React.Component<
  {
    FallbackComponent: React.ComponentType<FallbackProps>;
  },
  ErrorBoundaryState
> {
  state: ErrorBoundaryState = {
    error: null,
  };

  static getDerivedStateFromError(error: Error) {
    return { error };
  }

  render() {
    const { error } = this.state;

    if (error) {
      return <this.props.FallbackComponent error={error} />;
    }

    return this.props.children;
  }
}

function ErrorBoundaryFallback({ error }: FallbackProps) {
  return (
    <div role="alert">
      Something went wrong! 💣💥 <div>{error.message}</div>
    </div>
  );
}
```

By the way, the same prop exists in [react-error-boundary](https://github.com/bvaughn/react-error-boundary) so you could just use **ErrorBoundary** which is provided by this module
