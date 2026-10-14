```
import Control.Monad.Reader.Class (class MonadAsk, ask) ①
import Data.Api.Logoff (LogoffRequest(..), LogoffResponse(..)
    , LogoffResults(..))
import Data.Either (Either(..))
import Effect.Ref as Ref
import Env (Env)
import Utils (apiCall)

component
  :: ∀ m
  . MonadAff m
  => MonadAsk Env m ②
  => Navigate m Route
  => H.Component Query Input Output m
component = H.mkComponent
  { initialState: \_ ->
    { loggedOff: false
    , errorMessage: Nothing
    }
  , render
  , eval: H.mkEval H.defaultEval
    { initialize = Just Initialize ③
    , handleAction = handleAction
    }
  }
where
handleAction :: Action -> H.HalogenM State Action Slots Output m Unit
handleAction = case _ of
  Initialize -> do ④
    { userRef } <- ask
    loggedOnUser' <- H.liftEffect $ Ref.read userRef
    loggedOnUser' # maybe (pure unit) \{ authToken } -> do ⑤
      logoffResponse <- apiCall (LogoffRequest { authToken })
      case logoffResponse of
        Left err -> H.modify_ _ { errorMessage = Just err }
        Right (LogoffResponse LogoffResultsFailure) ->
          H.modify_ _ { errorMessage = Just $ "Unable to logoff" } ⑥
        Right (LogoffResponse LogoffResultsSuccess) -> do
          H.liftEffect $ Ref.write Nothing userRef ⑦
          H.modify_ _ { loggedOff = true } ⑧
-- BELOW CODE REDACTED
```

① Added these imports.